---
name: comment-doc
description: Review comments and documentation in the current branch diff for maintainable intent, comment rot, and missing interface context. Use when reviewing comments or docs, when comments repeat code, or when documentation needs a quality audit.
allowed-tools:
  - Read
  - Grep
argument-hint: "[file or module path]"
disable-model-invocation: true
---

# Comments & documentation review

Review comments in the current branch's diff. When `$ARGUMENTS` names a file or module, limit the review to it. Read the target code and enough surrounding context to understand each comment before reporting a finding.

Code records mechanism. Comments record information a first-time reader cannot infer from the code: intent, constraints, boundaries, ownership, units, preconditions, and cross-module dependencies.

## Scope

1. Inspect the diff and identify every touched file. If an argument narrows the target, use that scope instead.
2. Review every added or modified comment and documentation block in scope.
3. Sweep every comment in each touched file for ASCII banners, incidental history, defensive justification, correctness arguments, and stale facts that the diff exposes.
4. Read surrounding code before judging whether a comment repeats it.
5. Return only actionable findings. Report the file, line, and a concise addition, replacement, or deletion rationale. Do not edit files unless the user asks for an edit.

## Keep comments for meaning

A useful comment supplies information the code does not:

- **Interface:** the caller's mental model plus precise behavior, including units, ranges, ownership, nullability, ordering, and inclusive or exclusive bounds.
- **Implementation:** the high-level purpose of a non-obvious block or constraint, not a narration of statements.
- **Cross-module:** a dependency, protocol, or lifecycle rule whose participants live in separate modules.
- **Data member:** what a field represents beyond its type and name, including invariants and relations to other fields.

Flag a missing comment when readers need information the code cannot provide to use or safely change it. A public interface comment must let callers use the interface without reading its implementation. Add a concise comment when the diff introduces or exposes a durable, non-obvious constraint; do not add one merely to narrate the code.

## Remove comment rot and patch narration

Delete comments that describe the code's history rather than its current meaning. Comments must not use past-tense change verbs such as `added`, `removed`, or `changed`, and must not frame behavior as an increase, decrease, or other comparison with an unspecified former state.

Bad:

```ts
this.timeout(10_000); // Increase timeout for API calls
```

The comment gives neither a current constraint nor a reason for the value. A reader does not need to know what the timeout used to be. Delete it unless a non-obvious current constraint justifies a replacement.

Also delete comments such as:

- "This code now handles ..."
- References to today's bug, fix, regression, migration, or prior implementation.
- Defensive claims that the code is correct, safe, or required without documenting a durable constraint.
- Correctness arguments that merely restate the mechanism.
- ASCII banners and decorative separators.

When the durable reason matters, replace patch narration with that reason. Otherwise delete the comment.

## Apply the repeats-code test

Delete a comment when a first-time reader could write the same sentence by reading the surrounding code. Rephrasing an identifier is not explanation:

```ts
// Fetches the user profile.
fetchUserProfile(userId);
```

Treat comments as stale caches when they restate mutable facts from nearby code. Remove counts of subclasses, lists of variants, function call sites, implementation inventories, and any similar fact that changes when code changes. Follow DRY: the code is the source of truth for those facts.

Prefer a stable rule over a mutable inventory. For example, document the selection or compatibility constraint instead of listing every supported variant.

## Review questions

For each comment, ask:

1. Does this help a future maintainer understand intent or a non-obvious constraint?
2. Could the surrounding code state this just as well?
3. Does it describe current behavior rather than a version transition or bug fix?
4. Will its factual claims remain valid when routine code changes occur?
5. Is the comment concise enough that it describes the abstraction rather than leaking implementation details?

Delete when the answer to the first question is no or either of the next three indicates rot. Recommend a replacement only when a durable, non-obvious fact remains after removing the noise.

## Add missing context

Recommend an addition when code lacks durable context that a future maintainer needs but cannot infer:

- A public interface has non-obvious calling conditions, return semantics, units, ownership, bounds, ordering, or error behavior.
- A block encodes a non-obvious invariant, lifecycle requirement, compatibility constraint, or external-system behavior.
- A field has a meaning, resource owner, sentinel, unit, or relationship that its type and name do not convey.
- Code in separate modules relies on a protocol or ordering rule without a clear convergence point for that rule.

Write the smallest comment that states the enduring rule or reason. Do not add a comment for naming, control flow, a literal, a direct API call, or any fact visible in adjacent code. Do not turn the diff's present bug fix into a reason; name the stable constraint that remains after the fix.

## Findings format

Group findings by file. For each finding, use:

```text
path:line — Delete: "comment text"
Reason: Restates the adjacent code and contains no durable constraint.
```

For a replacement:

```text
path:line — Replace with: "replacement comment"
Reason: Records the resource-ownership invariant that callers cannot infer from the type.
```

For an addition:

```text
path:line — Add: "comment text"
Reason: Records the non-obvious ordering constraint between the producer and consumer.
```

If the review finds no actionable issues, state that the comments and documentation in scope provide durable, non-obvious context.
