---
name: principles-core
description: Core engineering principles for scoping and shaping any code change. Use before writing, fixing, refactoring, or reviewing code; when choosing libraries or dependencies; when sequencing a rewrite or migration; after repeated failed fixes; or when asked to be lazy, cut scope, or review for over-engineering.
---

# Core Principles

Each principle lives in its own file. Read every file whose trigger matches the work in front of you before acting; several usually apply at once. The laziness protocol applies to every coding task.

| Read | When |
|---|---|
| [laziness-protocol](laziness-protocol.md) | Any coding task. Climb the reuse-before-write ladder; bias toward deletion and the smallest change that works. |
| [subtract-before-you-add](subtract-before-you-add.md) | Sequencing an addition, refactor, or rewrite. Remove dead weight first. |
| [minimize-reader-load](minimize-reader-load.md) | Code is hard to trace: too many layers between question and answer, or too much hidden mutable state. |
| [foundational-thinking](foundational-thinking.md) | Before writing logic: picking core types and data structures, ordering scaffold vs feature work. |
| [redesign-from-first-principles](redesign-from-first-principles.md) | A new requirement lands in an existing design. Redesign as if it had been there from day one. |
| [attack-the-premise](attack-the-premise.md) | Two or more fixes sharing one assumption failed the same check. Question the assumption, not the next fix. |
| [exhaust-the-design-space](exhaust-the-design-space.md) | A novel UI interaction or architectural choice with no precedent here. Compare 2-3 real alternatives. |
| [experience-first](experience-first.md) | Product, UX, or feature-scope tradeoffs. User delight over implementation convenience. |
| [outcome-oriented-execution](outcome-oriented-execution.md) | Planned rewrites and migrations with phase boundaries. Converge on the end state, not smooth intermediate states. |
| [over-engineering-review](over-engineering-review.md) | Reviewing a diff or auditing a repo for what to delete, inline, or replace with stdlib or native features. |

Sibling principle skills: `principles-architecture` (types, state, APIs), `principles-verification` (tests, debugging, measurement, done-ness), `principles-workflow` (levers, delegation, asking the human, recurring corrections).
