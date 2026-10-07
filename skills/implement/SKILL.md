---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Build test-first where possible, at pre-agreed seams, following the test-first loop in /principles-verification.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, run /code-quality-review on the uncommitted changes before committing.

Commit your work to the current branch.
