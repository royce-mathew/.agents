# Attack the Premise

When two or more fixes that share one premise have failed the same gate, suspect the premise, not the fixes.

**Why:** Each failure under a shared premise is evidence about the premise.

**Pattern:**
- **Write the premise down.** The premise is the one sentence that every failed fix assumed.
- **Test the premise before the next fix.** Write a rerunnable probe, per [Build the Lever](../principles-workflow/build-the-lever.md), whose result would differ if the premise were false: feed the parser the input it supposedly never sees, call the API the way the fixes assume it behaves, count what the premise says is balanced. Run it on every case the fixes failed on.
- **A false premise is the next "why"** per [Fix Root Causes](../principles-verification/fix-root-causes.md). The failed fixes answered the wrong question; don't salvage them.
- **When the premise is balance across actors** (workers, shards, nodes), the probe is a census: record each actor's imbalance as a number, every run. If the same few actors hold most of it on every run, something assigns them that role. Find the assignment, then ask whether the role is intentional.
  - **Accidental role** (start order, hash skew, whoever grabs the lock first): remove the asymmetry instead of compensating for it, per the [Laziness Protocol](laziness-protocol.md). Rotate the role, randomize the assignment, or have actors pull from a shared pool instead of a fixed assignment. A return path, a batched hand-off of the excess, or a periodic rebalance leaves the assignment in place and adds work on every run.
  - **Intentional role** (single writer, leader, owner of an invariant): keep the owner. Make the role cheaper, or serialize access per [Separate Before Serializing Shared State](../principles-architecture/separate-before-serializing-shared-state.md). Spreading it breaks the invariant.

**Stop:**
- Do not start the next fix before the premise is written down and the probe has run.
- If the probe confirms the premise on every failing case, the premise is not the cause. Look elsewhere and keep the probe output as evidence.

This principle is distinct from [Redesign from First Principles](redesign-from-first-principles.md), which rebuilds a design around a new requirement. It questions a fact the current design assumes.
