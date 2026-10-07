# Over-engineering Review

Hunt complexity a diff or a repo doesn't need. One line per finding: location, what to cut, what replaces it. The best outcome is getting shorter. Lists findings, applies nothing.

**Scope:** a diff ("review for over-engineering", "what can we delete") or the whole tree ("audit this repo", "find bloat"). For a repo, rank findings biggest cut first.

**Scope boundary:** over-engineering only. Correctness bugs, security holes, and performance go to a normal correctness review. A single smoke test or `assert`-based self-check is the minimum, not bloat; never flag it.

## Tags

- `delete:` dead code, unused flexibility, speculative feature. Replacement: nothing.
- `stdlib:` hand-rolled thing the standard library ships. Name the function.
- `native:` dependency or code doing what the platform already does. Name the feature.
- `yagni:` abstraction with one implementation, config nobody sets, layer with one caller.
- `shrink:` same logic, fewer lines. Show the shorter form.

Repo-wide hunt list: deps the stdlib or platform already ships, single-implementation interfaces, factories with one product, wrappers that only delegate, files exporting one thing, dead flags and config, hand-rolled stdlib.

## Format

Diff: `L<line>: <tag> <what>. <replacement>.`, or `<file>:L<line>: ...` across files.
Repo: `<tag> <what to cut>. <replacement>. [path]`, ranked.

- `L12-38: stdlib: 27-line validator class. "@" in email, 1 line, real validation is the confirmation mail.`
- `L4: native: moment.js imported for one format call. Intl.DateTimeFormat, 0 deps.`
- `repo.py:L88: yagni: AbstractRepository with one implementation. Inline it until a second one exists.`
- `L52-71: delete: retry wrapper around an idempotent local call. Nothing replaces it.`
- `L30-44: shrink: manual loop builds dict. dict(zip(keys, values)), 1 line.`

A finding names the cut, never a question ("have you considered whether all these rules are needed?").

End with `net: -<N> lines possible.` (repo: `net: -<N> lines, -<M> deps possible.`). Nothing to cut: `Lean already. Ship.`
