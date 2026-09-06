# The Browser's Threads Optimizations

## 1. The Main Thread

The browser's main thread handles most application-facing work:

- JavaScript execution
- Event handlers and timers
- Network-response callbacks
- Framework/runtime work
- Style calculation
- Layout (reflow)
- Paint

A simplified rendering sequence is:

1. `requestAnimationFrame` callbacks
2. Style calculation
3. Layout
4. Paint
5. Compositing — handled by the compositor thread

JavaScript tasks run one at a time. While a task is executing, the browser cannot process another task, repaint, or respond to input.

### Frame budget

At 60 Hz, a frame is about **16.6 ms**. The practical application budget is roughly **10 ms** after browser overhead. At 120 Hz, the frame interval is only **8.3 ms**, so the available budget is even smaller.

A task lasting more than **50 ms** is generally considered a **long task**.

Main-thread blocking directly affects responsiveness metrics such as:

- **INP (Interaction to Next Paint):** responsiveness after user interaction.
- **TBT (Total Blocking Time):** accumulated main-thread blocking during loading.

The key principle:

> Performance is often less about making individual code faster and more about preventing important work from monopolizing the main thread.

---

# 2. Four Ways to Use the Main Thread Wisely

The article divides main-thread optimization into four techniques:

1. **Splitting** — make long tasks smaller.
2. **Batching** — combine frequent work.
3. **Prioritizing** — decide which work should run first.
4. **Deferring** — postpone work that does not need to happen immediately.

Splitting establishes task boundaries; batching controls how often work is performed; prioritizing and deferring control timing.

---

# 3. Splitting: Yield Long Tasks

If a large amount of work arrives at once, processing it as one synchronous task can freeze:

- rendering
- animations
- input
- event handling

Instead, divide the work into chunks and **yield** between them.

Example:

```js
async function renderChats(chats) {
  let count = 0;

  for (const chat of chats) {
    appendChatNode(chat);

    if (++count % 20 === 0) {
      await new Promise(resolve => setTimeout(resolve, 0));
    }
  }
}
```

Yielding does **not** reduce total computation. It can even increase wall-clock time slightly. Its benefit is responsiveness: the browser gets opportunities between tasks to process input and render frames.

## Split by count vs. time

Fixed-size chunks are simple, but when animation or scrolling is active, **time-based splitting** is safer.

```js
async function processDuringAnimation(items) {
  let i = 0;
  let frameStart = performance.now();

  while (i < items.length) {
    while (
      i < items.length &&
      performance.now() - frameStart < 5
    ) {
      doWork(items[i++]);
    }

    frameStart = await new Promise(requestAnimationFrame);
  }
}
```

The article uses approximately **5 ms per frame** as a heuristic, leaving room for animation callbacks, style, layout, and paint. It is not a magic number; reduce it when animation is expensive.

Using the timestamp supplied by `requestAnimationFrame` is important because other callbacks may already have consumed part of the frame budget.

## Yielding mechanisms

### `setTimeout`

Simple and widely supported, but it can introduce minimum scheduling delays.

### `MessageChannel`

Can be used to schedule continuations as tasks with finer control. React's scheduler uses this mechanism.

### `scheduler.yield()`

A newer API designed specifically for yielding. Its useful property is that the continuation can resume ahead of other queued tasks. Browser support is not yet universal.

### `requestAnimationFrame`

Best suited when work must remain synchronized with the rendering cycle.

## Important limitation

Some operations cannot be split internally. For example:

```js
JSON.parse(largeString);
```

is synchronous and effectively atomic from JavaScript's perspective. If parsing is expensive enough to block the UI, yielding around it does not solve the fundamental problem.

That is a signal to move the work away from the main thread.

---

# 4. Batching: Reduce Fixed Overhead

Splitting improves responsiveness but does not necessarily improve throughput.

If work arrives faster than it can be processed, a **backlog/backpressure** develops.

Batching combines multiple operations so their fixed overhead is paid fewer times.

Typical high-frequency event sources:

- `scroll`
- `resize`
- pointer/input events
- streaming data
- repeated UI updates

Batching also applies to DOM writes and state updates: collect multiple changes and apply them together so fixed rendering/reconciliation costs are paid fewer times.

Two fundamental patterns are:

### Debounce

Run after activity becomes quiet.

Useful when only the final state matters.

Example use: rebuilding a preview after the user stops typing.

### Throttle

Run at most once per specified interval.

Useful when updates should continue during sustained activity but at a controlled rate.

### Splitting vs. batching

They solve different problems:

| Problem | Technique |
|---|---|
| One task is too long | Splitting |
| Tasks arrive too frequently | Batching |
| Work is not urgent | Deferring |
| Multiple tasks compete | Prioritizing |

They can and often should be combined.

---

# 5. Prioritizing

Not all work has equal value to the user.

When multiple tasks compete for the main thread, favor work that directly affects the current interaction or visible state.

Typical high-priority work:

- responding to input
- updating visible UI
- maintaining interaction feedback
- animation-related work

Lower-priority work may include:

- secondary calculations
- non-visible updates
- analytics
- background processing
- preparation for future interactions

A practical implementation is a work queue: normal jobs can be processed FIFO, while urgent jobs can be promoted to the front when user interaction makes them immediately relevant. This is the **idle-until-urgent** pattern.

Modern browsers also expose scheduling primitives such as the Scheduler API and `TaskController`, although support is still incomplete.

The objective is not necessarily to execute less work, but to ensure that **important work gets access to the main thread first**.

---

# 6. Deferring

Some work is necessary but does not need to happen now.

Defer it until:

- the current interaction finishes
- the browser has an opportunity to render
- the work becomes relevant
- the main thread is less busy

Useful deferral techniques include:

- **Code splitting:** load/execute only the code needed by the current screen, then load other code when required.
- **`IntersectionObserver`:** create/fill expensive content as it approaches the viewport rather than rendering everything immediately.
- **`content-visibility: auto`:** allows the browser to skip work for content that is not relevant to the current viewport; engine behavior should still be tested.
- Stop continuously running animations, charts, and other work while they are off screen.

Deferring prevents non-urgent work from competing with immediate user-visible operations.

Splitting and deferring complement each other:

- **Splitting:** “Don't block for too long.”
- **Deferring:** “Don't run this yet.”

---

# 7. Avoid the Main Thread When Possible

The second major strategy is not to optimize use of the main thread, but to **remove work from it**.

The article describes three approaches:

1. Move work to the compositor.
2. Send work to a Web Worker.
3. Eliminate unnecessary work entirely.

---

# 8. Move Work to the Compositor

Some visual operations can be handled without repeatedly running the expensive main-thread rendering pipeline.

CSS animations involving compositor-friendly properties such as:

- `transform`
- `opacity`

can continue animating while the main thread is blocked, provided the browser can keep the animation on the compositor.

This explains why a CSS animation can continue while JavaScript-driven animation freezes.

Prefer compositor-friendly animation when possible.

A useful conceptual distinction is:

```text
Main thread:
JavaScript → style → layout → paint

Compositor:
already-produced visual layers → composition → screen
```

The goal is to avoid forcing every animation frame through JavaScript, layout, and paint.

## FLIP for layout-changing animations

When an animation genuinely represents a layout change, **FLIP (First, Last, Invert, Play)** can move the per-frame animation work to `transform`:

1. **First:** measure the original position.
2. **Last:** perform the layout change and measure the new position.
3. **Invert:** apply a transform that visually returns the element to its original position.
4. **Play:** animate the transform back to its identity value.

This causes the layout change once and lets the animation itself use compositor-friendly transforms.

## Avoid layout thrashing

Do not repeatedly interleave layout reads and writes:

```js
for (const el of elements) {
  const width = el.offsetWidth;
  el.style.width = width + 10 + 'px';
}
```

Prefer grouping reads first and writes second. Interleaving them can force repeated synchronous layout recalculation.

`will-change: transform` can hint that an element should be prepared for compositor animation, but excessive use can increase layer count and memory consumption.

---

# 9. Send Work to a Web Worker

CPU-heavy computation that does not need direct DOM access can be moved to a **Web Worker**.

This keeps the main thread available for:

- rendering
- input
- interaction
- event processing

Typical worker candidates include:

- computationally expensive algorithms
- parsing/transformation
- data processing
- large calculations

Workers cannot directly manipulate the DOM. Communication occurs by passing messages.

## Transferable Objects

Copying large data between the main thread and a worker can itself be expensive.

For large binary data, use **Transferable Objects** when appropriate. Ownership of the underlying buffer can be transferred instead of copying its contents.

This is particularly useful for large `ArrayBuffer`-based datasets. After an `ArrayBuffer` is transferred, the sender can no longer use that buffer (it becomes detached), so transfer is a trade-off rather than a free optimization.

The architectural goal is:

```text
Main thread
    │
    │ message / transferable data
    ▼
Worker
    │
    │ computation
    ▼
Main thread
```

The worker should do enough useful computation to justify the communication overhead.

---

# 10. Eliminate the Work

The best optimization is often to avoid doing the work at all.

The article highlights several forms of elimination.

## Dropping

If intermediate states are no longer useful, discard them.

Example: if ten updates arrive while the UI is busy but only the newest state matters, processing all ten may be unnecessary.

## Merging

Combine multiple updates into one equivalent operation.

Example:

```text
update A
update B
update C
```

may be replaceable by:

```text
apply final state
```

## Skipping

The article's third category is **skipping repeated work**: if the same computation with the same input would produce the same result, do not perform it again.

A related example is avoiding work for content that is not currently visible.

## Memoization

Cache results of expensive computations when the same inputs recur.

Instead of:

```text
same input → recompute
same input → recompute
same input → recompute
```

use:

```text
same input → cached result
```

The general rule is:

> Before optimizing a computation, ask whether the computation needs to happen at all.

---

# 11. Combining the Techniques

Real applications often need several techniques simultaneously.

A high-frequency pipeline might look like:

```text
Incoming events
      │
      ▼
   Batch
      │
      ▼
 Drop / merge obsolete updates
      │
      ▼
 Prioritize user-visible work
      │
      ▼
 Split expensive processing
      │
      ├──► Main thread: UI-critical work
      │
      └──► Worker: CPU-heavy computation
      │
      ▼
 Compositor-friendly rendering
```

A practical strategy is:

1. **Eliminate** unnecessary work.
2. **Batch** work that is too frequent.
3. **Prioritize** user-visible work.
4. **Defer** work that is not urgent.
5. **Split** remaining long tasks.
6. **Move** CPU-heavy work to a Worker.
7. **Use compositor-friendly rendering** for animations where possible.
8. **Avoid layout thrashing** by grouping layout reads and writes.

---

# 12. Practical Rules

### Keep tasks short

A long synchronous task blocks everything else on the main thread.

### Don't confuse throughput with responsiveness

Yielding can make a job take longer while making the application feel much faster.

### Don't split too aggressively

Every yield has overhead. Excessively tiny chunks can reduce throughput.

### Don't blindly use `setTimeout`

Its scheduling behavior may introduce unnecessary delays. Choose the scheduling primitive according to the workload.

### Synchronize frame-sensitive work with `requestAnimationFrame`

Especially when the goal is to cooperate with the browser's rendering cycle.

### Watch for non-splittable operations

Large synchronous parsing or computation may require a Worker rather than more yielding.

### Prefer CSS/compositor animation when appropriate

Avoid unnecessary JavaScript work on every frame.

### Treat data movement as work

Worker communication and copying large objects can become bottlenecks.

### Optimize what the user experiences

The objective is not merely maximum computation throughput. It is responsive input, timely feedback, and smooth rendering.

---

# 13. Core Mental Model

The article's central idea can be reduced to one question:

> **How much of the main thread do I occupy, how often, and when?**

There are four ways to improve that allocation:

```text
Too long?       → SPLIT
Too frequent?   → BATCH
Wrong order?    → PRIORITIZE
Not urgent?     → DEFER
```

And three ways to avoid the main thread:

```text
Visual work     → COMPOSITOR
CPU work        → WORKER
Unnecessary work→ ELIMINATE
```

The ultimate goal is not to make every operation fast.

It is to ensure that **the browser always has enough opportunity to render and respond to the user.**
