---
name: principles-workflow
description: Agent workflow principles for how work gets done. Use when facing non-trivial edits, migrations, or analyses that a script, codemod, or generator could do; fanning work out to subagents; context filling with large outputs; deciding whether to ask the human before acting; or after the same correction or instruction comes up twice.
---

# Workflow Principles

Each principle lives in its own file. Read every file whose trigger matches the work in front of you before acting; several usually apply at once.

| Read | When |
|---|---|
| [build-the-lever](build-the-lever.md) | Any non-trivial edit, migration, analysis, or check. Build the tool that does or proves it instead of working by hand. |
| [guard-the-context-window](guard-the-context-window.md) | Large outputs, long files, repeated reads, or fan-out planning. Route bulk to subagents; keep summaries. |
| [never-block-on-the-human](never-block-on-the-human.md) | Tempted to ask "should I do X?" on reversible work. Proceed and present; confirm only irreversible actions. |
| [encode-lessons-in-structure](encode-lessons-in-structure.md) | The same instruction or correction comes up a second time. Encode it as a lint, type, check, or script. |

Sibling principle skills: `principles-core` (scoping and shaping any change), `principles-architecture` (types, state, APIs), `principles-verification` (tests, debugging, measurement, done-ness).
