---
name: principles-architecture
description: Architecture principles for types, state, and APIs. Use when designing types or data models, writing stateful or branch-heavy logic, wiring validation or error handling, building commands or loops that must survive crashes and retries, replacing an internal API, or letting concurrent actors share a file, key, or state object.
---

# Architecture Principles

Each principle lives in its own file. Read every file whose trigger matches the work in front of you before acting; several usually apply at once.

| Read | When |
|---|---|
| [model-the-domain](model-the-domain.md) | Stateful logic, code that branches a lot, or a shape assumption repeated across files. Encode the domain in a structure. |
| [boundary-discipline](boundary-discipline.md) | Wiring validation, error handling, or framework adapters. Guard at system boundaries; trust internal types. |
| [type-system-discipline](type-system-discipline.md) | Designing types, reviewing a signature, or writing in any statically-typed language. |
| [make-operations-idempotent](make-operations-idempotent.md) | Commands, lifecycle steps, or processing loops that run amid crashes, restarts, and retries. |
| [migrate-callers-then-delete-legacy-apis](migrate-callers-then-delete-legacy-apis.md) | A new internal API while old callers still exist. Migrate and delete in the same wave. |
| [separate-before-serializing-shared-state](separate-before-serializing-shared-state.md) | Concurrent actors might write the same file, branch, key, or state object. Remove the sharing before adding a lock. |

Sibling principle skills: `principles-core` (scoping and shaping any change), `principles-verification` (tests, debugging, measurement, done-ness), `principles-workflow` (levers, delegation, asking the human, recurring corrections).
