# Comment Style

Match the existing codebase voice.

- Comment the reason, lifecycle risk, tradeoff, or user-visible consequence that code alone does not reveal.
- Use plain, concrete language: name the specific provider, route, state, listener, or UI behavior involved.
- Write natural sentence fragments or short sentences. Expand into a compact paragraph only when explaining a causal chain.
- Keep comments local to the decision they explain and update them with the behavior they describe.
- Preserve useful existing comments through refactors; rewrite them when the implementation changes their meaning.
- Prefer the codebase's conversational technical tone over framework jargon. Explain what can go wrong and why this code prevents it.
