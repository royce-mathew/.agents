---
name: principles-verification
description: Verification principles for tests, debugging, measurement, and done-ness. Use when writing, changing, or keeping a test; building test-first (TDD, red-green); debugging; running a sweep or migration of similar edits; stacking commits; reporting a benchmark, speedup, regression, or eval number; or before declaring a task done.
---

# Verification Principles

Each principle lives in its own file. Read every file whose trigger matches the work in front of you before acting; several usually apply at once.

| Read | When |
|---|---|
| [prove-it-works](prove-it-works.md) | Before declaring any task done. Check the real artifact, not a proxy. |
| [fix-root-causes](fix-root-causes.md) | Debugging. Reproduce, ask why until the root cause, fix it where every caller routes through. |
| [sequence-verifiable-units](sequence-verifiable-units.md) | Multi-step work (sweeps, migrations, runs of similar edits) and stacking commits or PRs. |
| [test-behavior-not-implementation](test-behavior-not-implementation.md) | Writing, changing, or keeping a test, choosing seams and mocks, or building test-first (TDD). |
| [explain-the-number](explain-the-number.md) | Before trusting, reporting, or acting on a measured number. For performance numbers it routes to the [benchmark checklist](benchmark-checklist.md). |

Sibling principle skills: `principles-core` (scoping and shaping any change), `principles-architecture` (types, state, APIs), `principles-workflow` (levers, delegation, asking the human, recurring corrections).
