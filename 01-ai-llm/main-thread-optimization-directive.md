# Main-Thread Optimization Directive (Agent/LLM Operational Guide)

## Purpose
Use this directive when writing, reviewing, or refactoring browser-side JavaScript that touches rendering, animation, high-frequency events, or heavy computation. Apply it as a checklist, not as background theory.

## Core Principle
- The browser main thread is a single shared queue for JavaScript execution AND rendering (style, layout, paint).
- A running task cannot be interrupted; nothing else (input, repaint, other code) runs until it finishes.
- Frame budget: ~10 ms usable at 60 Hz, roughly half that (~5 ms) at 120 Hz. Any task over 50 ms is a "long task" and a defect.
- Main-thread blocking directly shows up in responsiveness metrics: INP (Interaction to Next Paint) and TBT (Total Blocking Time). Treat regressions in either as a main-thread problem first.
- Goal is not raw computation speed — it is keeping the main thread free enough to respond and render on time.
- Yielding/splitting does NOT reduce total work and can slightly increase wall-clock completion time. Its only benefit is responsiveness. Do not confuse throughput with responsiveness — they are different goals and are optimized differently.

## Diagnostic Questions (ask before writing code)
- Does this work run on every event/tick, or only when needed? → if "every time", suspect missing batching or deferring.
- Could this task exceed the frame budget (~10 ms, or as little as ~5 ms if sharing the frame with active animation) in one synchronous pass? → if yes, it needs splitting or must move off-thread.
- Does this work affect what the user currently sees/interacts with? → if no, it is deferrable/low-priority by default.
- Is this computation CPU-heavy and DOM-independent? → candidate for a Web Worker.
- Is this a visual animation using only transform/opacity? → candidate for compositor-only animation, skip JS/layout entirely.
- Would dropping, merging, or caching this update produce the same visible outcome? → eliminate the work before optimizing it.

## Directive 1 — Split Long Synchronous Work
- Never let a single synchronous task exceed the frame budget (~10 ms generally, ~5 ms when other animation work shares the same frame).
- Break large loops/batches into chunks and yield control between chunks.
- Prefer time-based chunking (stop after a time budget, resume next frame) over count-based chunking when animation or scrolling may be active concurrently.
- Match the yielding mechanism to the requirement:
  - `requestAnimationFrame` — best when work must stay in sync with the rendering cycle.
  - `scheduler.yield()` — newer API; continuation resumes ahead of other queued tasks instead of going to the back of the line. Support is not yet universal.
  - `MessageChannel` — posts a message to schedule the continuation as a new task with finer control; used internally by frameworks such as React's scheduler.
  - `setTimeout` — simplest and most widely supported, but introduces a minimum scheduling delay; do not use it by default when precision timing matters.
- Do not over-split: each yield has overhead; excessive fragmentation reduces throughput without improving responsiveness.
- Recognize non-splittable synchronous operations (e.g., parsing a very large payload in one call, such as a large `JSON.parse`). If yielding around it doesn't help, do not keep trying to split it — move it off the main thread instead.

## Directive 2 — Batch Frequent Work
- Identify high-frequency triggers: scroll, resize, pointer/input events, streaming data ticks, repeated state updates.
- Never run an expensive handler on every single firing of a high-frequency event.
- If arrivals outpace processing, a backlog builds up and the screen shows increasingly stale state — this is backpressure. Batching is the fix.
- Collapse repeated triggers into one execution using:
  - Debounce — run once after activity goes quiet; use when only the final state matters.
  - Throttle — run at most once per fixed interval; use when updates should continue during sustained activity but at a controlled rate.
- Batch DOM writes and state updates: accumulate changes, apply them together, avoid one-write-per-change patterns. For continuous visual updates, coalesce to at most once per rendered frame.
- Distinguish the failure mode: if the task is too long, split it; if it fires too often, batch it. Apply both when both conditions exist.

## Directive 3 — Prioritize User-Relevant Work
- Rank work by relevance to what the user is currently doing or seeing.
- High priority: direct response to input, visible UI updates, active interaction feedback, active animation.
- Low priority: background/off-screen computation, analytics, precomputation for future actions, non-visible updates.
- When multiple tasks compete, structure execution as a queue where urgent work can preempt or jump ahead of queued non-urgent work rather than waiting in strict FIFO order.
- Reassess priority dynamically: work that was low priority can become urgent the moment the user interacts with it directly (e.g., requesting the specific item now). Precomputing while idle and promoting to the front on demand is known as the idle-until-urgent pattern.
- Modern browsers expose scheduling primitives for this purpose — the Scheduler API and `TaskController` — though support is still incomplete; a hand-built priority queue is an acceptable fallback.
- The objective is ordering, not reducing total work — do the same work, but in the order that matches user attention.

## Directive 4 — Defer Non-Urgent Work
- Do not perform work now if it can correctly happen later without harming the user experience.
- Defer until: the current interaction completes, the browser has idle capacity, the content becomes relevant (e.g., enters viewport), or the main thread is less busy.
- Applicable deferral tactics:
  - Code splitting — load/execute only the code required for the current view; load the rest on demand.
  - `IntersectionObserver` — create/fill expensive content only as it approaches the viewport rather than rendering everything up front.
  - `content-visibility: auto` — allows the rendering engine to skip work for off-screen content where supported; verify actual engine behavior rather than assuming it.
  - Pause or stop animations, charts, or polling loops that are off-screen or inactive.
- Splitting says "don't block for too long"; deferring says "don't run this yet." Use both together where applicable.

## Directive 5 — Move Visual Work to the Compositor
- Prefer animating only compositor-friendly properties (transform, opacity) instead of properties that force layout/paint every frame.
- Compositor-only animations can continue running even while the main thread is blocked; layout/paint-driven animations cannot — this is why a CSS transform/opacity animation keeps running while JS-driven animation freezes.
- For animations that appear to require a layout change, use the FLIP technique (First, Last, Invert, Play): measure the original position, perform the layout change and measure the new position, apply a transform that visually inverts back to the original position, then animate that transform to its identity value. This makes the layout change happen once, while the animation itself stays on the compositor.
- Never interleave reading layout values and writing styles in the same loop iteration; group all reads first, then all writes, to avoid forced synchronous layout recalculation (layout thrashing).
- `will-change: transform` can hint that an element should be prepared for compositor animation, but use it sparingly — excessive use increases layer count and memory consumption.

## Directive 6 — Offload CPU Work to a Worker
- Move computation that is CPU-heavy and does not require direct DOM access off the main thread, into a Web Worker.
- Typical candidates: expensive algorithms, large-scale parsing/transformation, heavy data processing.
- Remember workers cannot touch the DOM directly; communication is message-based only.
- Treat data transfer itself as a cost: copying large data between main thread and worker can be expensive on its own.
- For large binary datasets (e.g., `ArrayBuffer`-based data), use Transferable Objects to move ownership instead of copying — but note the sending side loses access to that buffer once transferred (it becomes detached), so this is a trade-off, not a free win.
- Only offload when the computation is heavy enough to justify the message-passing/transfer overhead; trivial work sent to a worker can be a net loss.

## Directive 7 — Eliminate Work Before Optimizing It
- Before applying any of the above techniques, check whether the work needs to happen at all.
- Dropping: if intermediate states are superseded before they're ever used, skip processing them — only the latest matters.
- Merging: combine a sequence of incremental updates into a single equivalent final update instead of applying each one individually.
- Skipping: do not repeat a computation when the same input would produce the same result; do not process content that is not currently visible or relevant.
- Memoization: cache results of expensive computations keyed by input, and reuse cached results on repeated identical input.
- Always ask "does this need to run at all?" before asking "how do I make this run faster?"

## Combined Execution Order (recommended default sequence)
1. Eliminate unnecessary work first (drop/merge/skip/cache).
2. Batch remaining work that fires too frequently.
3. Prioritize what directly affects current user-visible state.
4. Defer everything that is not immediately needed.
5. Split whatever long synchronous work remains.
6. Offload heavy CPU-only computation to a Worker.
7. Render animations using compositor-friendly properties wherever possible.
8. Group layout reads and writes to avoid thrashing.

## Anti-Patterns to Flag and Correct
- A single task that can run longer than ~50 ms without yielding.
- A handler bound to a high-frequency event (scroll/resize/input/stream) with no debounce/throttle/batching.
- JavaScript-driven per-frame animation of layout-affecting properties when transform/opacity would achieve the same visual result.
- Interleaved layout read/write loops (read, write, read, write) instead of grouped reads then writes.
- CPU-heavy synchronous computation left on the main thread when it has no DOM dependency.
- Recomputing or re-rendering identical output for identical input instead of caching.
- Excessive micro-splitting of trivial work, adding yield overhead with no responsiveness benefit.
- Defaulting to `setTimeout` for yielding when precision or resume-priority actually matters.

## Success Criteria
- No single synchronous task blocks the main thread beyond the frame budget.
- INP and TBT stay within acceptable bounds; no long tasks (>50 ms) go unaddressed.
- User input and visible UI updates are never starved by background or non-visible work.
- Animations remain smooth even when other main-thread work is in progress, wherever compositor-only animation is feasible.
- Heavy computation is either eliminated, cached, batched, deferred, split, or moved to a Worker — never left as one large blocking call.
