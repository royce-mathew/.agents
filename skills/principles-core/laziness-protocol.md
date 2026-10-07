# Laziness Protocol

Aim for the most result with the least code and complexity. Lazy means efficient, not careless: the best code is the code never written.

## The ladder

Stop at the first rung that holds:

1. **Does this need to exist at all?** Speculative need = skip it, say so in one line. (YAGNI)
2. **Already in this codebase?** A helper, util, type, or pattern that already lives here → reuse it. Look before you write; re-implementing what's a few files over is the most common slop.
3. **Stdlib does it?** Use it.
4. **Native platform feature covers it?** `<input type="date">` over a picker lib, CSS over JS, DB constraint over app code.
5. **Already-installed dependency solves it?** Use it. Never add a new one for what a few lines can do.
6. **Can it be one line?** One line.
7. **Only then:** the minimum code that works.

The ladder runs *after* you understand the problem, not instead of it. Read the task and the code it touches, trace the real flow end to end, then climb. Two rungs work → take the higher one. The smallest change in the wrong place isn't lazy, it's a second bug.

## Rules

- **Prefer deletion.** When asked to refactor or improve, look for removals before additions.
- **Maintain a flat call hierarchy.** Avoid deep call chains. A rich interface that hides substantial work is not a deep call chain. If answering a question requires tracing through more than 3 files or layers, flatten it.
- **Consolidate decisions.** Do not repeat the same choice in several places. Put it behind one source of truth and pass the result as a simple flag.
- **Minimize the diff.** Make the smallest change that solves the problem. Fewer lines beat "elegant" boilerplate.
- **Question the threading.** If a task asks you to pass a new signal through types, schemas, pipelines, or similar layers, stop and look for a more direct path.
- **Sweat the small leaks.** Remove tiny pass-throughs, representation leaks, and duplicated choices before they spread. Small leaks compound into permanent coordination costs.
- **No unrequested abstractions.** No interface with one implementation, no factory for one product, no config for a value that never changes, no scaffolding "for later". Boring over clever.
- **Fewest files possible.** Two stdlib options of the same size? Take the one that's correct on edge cases. Lazy means writing less code, not picking the flimsier algorithm.
- **Ship the lazy version and question it in the same response:** "Did X; Y covers it. Need full X? Say so." Never stall on an answer you can default.
- **Mark deliberate corner-cuts.** A simplification with a known ceiling (global lock, O(n²) scan, naive heuristic) gets a comment naming the ceiling and the upgrade path: `# global lock; per-account locks if throughput matters`.
- **Report skipped scope in one line:** `skipped: X, add when Y.` No essays defending a simplification; that's complexity smuggled back in as prose. Explanation the user asked for is not debt.

**The test:** If a human developer would find the code exhausting to maintain, it is a bad solution.

## Never simplify away

- Input validation at trust boundaries, error handling that prevents data loss, security measures, accessibility basics, anything explicitly requested. User insists on the full version → build it, no re-arguing.
- Understanding. The ladder shortens the solution, never the reading. Laziness that skips comprehension ships a confident wrong fix.
- Calibration for physical hardware. A real clock drifts, a real sensor reads off; leave the tuning knob a minimal model can't see.
- The check. Non-trivial logic (a branch, a loop, a parser, a money or security path) leaves one runnable check behind: the smallest thing that fails if the logic breaks. Trivial one-liners need none.
