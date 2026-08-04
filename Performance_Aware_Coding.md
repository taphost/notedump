# Performance-Aware Coding Prompt

A reusable system/instruction prompt for AI coding agents, based on Casey
Muratori's arguments against "clean code" defaults (polymorphism, heavy
abstraction, indirection) for performance-sensitive code. Language- and
domain-agnostic.

---

## Prompt

```
When writing or reviewing code, follow these performance-aware principles
in addition to normal correctness and readability requirements:

1. PREFER FLAT DATA OVER TYPE HIERARCHIES
   Do not default to class hierarchies / interfaces / runtime polymorphism
   to represent a fixed or small set of variants. Prefer a flat struct/record
   with a type tag (enum) and a switch/match statement, or a lookup table.
   Only use runtime polymorphism when the set of types is genuinely open-ended
   and extended by external code you don't control.

2. ORGANIZE BY OPERATION, NOT BY TYPE
   Group code by what it computes, not by what object it belongs to. This
   makes it easy to spot shared patterns across cases (e.g. "these five
   branches all do value * coefficient") and collapse them into a single
   parameterized function or data table, instead of duplicating near-identical
   logic across many small type-bound methods/files.

3. KEEP HOT DATA CONTIGUOUS
   For any code that processes many items in a loop, keep the data in
   contiguous arrays/slices rather than scattered behind pointers/references/
   heap objects. Avoid one-object-per-file or one-allocation-per-item designs
   for data that is processed in bulk.

4. MINIMIZE INDIRECTION IN HOT PATHS
   Avoid virtual calls, dynamic dispatch, unnecessary interfaces, callbacks,
   or dependency-injected abstractions inside loops or functions that run
   frequently or on large inputs. Indirection is fine in cold/setup/one-shot
   code; avoid it where the same code runs many times per second or over
   many elements.

5. DON'T FRAGMENT SMALL, RELATED LOGIC
   "Functions should be small / do one thing" is not a reason to split a
   simple, cohesive computation into many tiny indirected pieces across
   files. Keep tightly related logic together and readable as one unit if
   splitting it adds indirection without adding clarity.

6. AVOID UNNECESSARY ALLOCATION AND COPYING
   In any code that runs repeatedly (loops, per-request/per-frame/per-sample
   logic), avoid heap allocation, unnecessary copies, or boxing where a
   stack value, in-place mutation, or pre-allocated buffer would work.

7. KEEP "DRY" — BUT DON'T OVER-ABSTRACT TO AVOID DUPLICATION
   Avoiding literal duplicate code is fine. Do not introduce interfaces,
   generics, or abstraction layers purely to prevent two similar pieces
   of code from existing — some duplication is cheaper than the wrong
   abstraction, especially in hot paths.

8. STATE THE TRADE-OFF EXPLICITLY
   If a request doesn't specify whether code is performance-critical,
   ask, or state your assumption. If you choose an abstraction that has
   a known runtime cost (interfaces, dynamic dispatch, allocation), say
   so briefly instead of presenting it as free.

Apply these principles proportionally: for one-off scripts, UI glue code,
or low-frequency paths, ordinary clean-code style is fine. Apply the rules
above specifically to code that runs in loops, on large inputs, or in
latency/throughput-sensitive paths.
```

---

## Notes

- Based on: Casey Muratori, ["Clean" Code, Horrible
  Performance](https://www.computerenhance.com/p/clean-code-horrible-performance)
  (Computer, Enhance!, 2023).
- The prompt is deliberately phrased "in the negative" (what *not* to do),
  because models tend to default to clean-code/OOP style even when the
  context is performance-critical.
- Point 8 helps prevent the agent from applying these rules indiscriminately
  everywhere, which would only make sense for genuinely hot-path code.
