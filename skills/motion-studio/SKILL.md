---
name: motion-studio
description: Create or revise code-rendered motion videos, product launch films, reels, UI morph loops, explainers, or their production pipeline. Use when deterministic rendering, reference-led art direction, beat-synced audio, or frame-by-frame critique is required.
---

# Motion Studio

Make films from a **timeline**, not a one-shot prompt. The deliverable is a deterministic render pipeline and an inspected video—not merely animation source that appears plausible.

## Intake

Establish the brief from the user's request and available material before writing animation code:

- **Purpose and viewer:** showreel, product launch, explainer, story, or loop; desired feeling; duration; primary format.
- **Truth sources:** product URL and access, real UI/screenshots/logo/fonts/colors, metrics and exact copy. For a product film, real captured UI is mandatory; never draw a fictional product interface.
- **Direction:** reference frame, film, or image library; what to borrow (visual grammar) and what remains original (subject, marks, characters, content).
- **Sound:** supplied track, licensed source, or code-synthesized score; voice/mascot only when explicitly requested and credentials are available through environment variables.
- **Constraints:** existing renderer/framework, output formats, loop requirement, runtime/budget, and whether this is a short clip or a flagship film.

Use supplied answers; do not repeat questions. If a non-brand creative detail is missing, choose a deliberate default and state it in the shot list. If the missing information would force invented product truth, inaccessible assets, or a wrong public claim, ask for it before that part of production.

Read [PRODUCTION.md](PRODUCTION.md) to create the appropriate reference, brand, state-morph, or long-form brief.

## Choose the production route

Reuse the project's established route. Otherwise choose the smallest route that satisfies the brief:

- **Seek renderer (default):** HTML canvas or DOM/SVG with `window.seek(t)`. Best for a one-off, bespoke graphic film with minimal dependencies.
- **Remotion:** existing React video projects, repeatable templates, data-driven series, or substantial component reuse.
- **HyperFrames or an established HTML animation stack:** projects already authored as web pages or explicitly requiring its capabilities.

Do not add a framework merely because it exists. If no render project exists, inspect the installed runtime and tools first; install only the actual dependencies the selected route needs.

## Production gates

Execute these gates in order. Save project artifacts in existing conventions; otherwise use `assets/`, `docs/`, `src/`, and `out/`.

1. **Discover.** Capture source assets into `assets/`; identify real fonts, colors, copy, screenshots, and usage constraints. With a reference, extract representative frames and write `docs/style_guide.md`. Its single job is to turn the reference's grammar into actionable palette, type, cadence, transition, camera, and texture decisions.
2. **Direct.** Write `docs/shotlist.md` before detailed animation: time range, beat, purpose, frame composition, movement, text, source assets, transition, and sound cue for every shot. Make the first two seconds carry the hook; provide a visibly new payoff every 2–4 seconds. For a loop, define the identical first and final state—including cursor position and velocity.
3. **Build the timeline.** Use the chosen route to implement the render contract in [ENGINE.md](ENGINE.md). Derive every format from the same semantic timeline and layout system; recompose type and UI per format rather than cropping a landscape render into vertical.
4. **Make sound part of the edit.** Measure a supplied track or synthesize score and effects on the same timebase. Put cuts and deliberate events on the actual beat grid, then mix as specified in [ENGINE.md](ENGINE.md).
5. **Inspect and correct.** Render the review artifacts, inspect pixels at full composition and phone size, score the work, and correct the three worst observed problems. Follow [REVIEW.md](REVIEW.md); complete at least three critique passes for a flagship or explicitly high-polish film.
6. **Render and deliver.** Produce final encoded media in every requested format plus the contact sheet, poster frame, source, and any loop check. Report real assets used, remaining assumptions, review scores, and any known limitation—never an invented completion claim.

A short unbranded showreel may combine gates 1–3 after a lightweight direction choice. A branded, reference-led, or long-form film must preserve the written style guide and shot list as production records.

## Look rules

Compose a specific visual system: one display face, one UI face when UI is present, a disciplined palette, and a clear compositional hierarchy. Motion should reveal, transform, or reframe information; use cuts, masks, camera moves, scale, paths, and morphs where each is motivated by the shot.

Avoid generic visual defaults: centered title over an undirected gradient, universal fade-ins, decorative corner labels/borders, glowing UI chrome, and untethered particle bursts. State the positive alternative in the shot list for each scene: its anchor, visual device, and transition.

## Operating mode

- **Setup proof:** a 10–15 second showreel can validate a new renderer, but it is not product direction. Start real work from a brief, reference, or state list.
- **State-morph films:** maintain one recognisable container through states; a cursor drives meaningful interactions. Content arrives after its container begins to morph and leaves before the next morph. See [PRODUCTION.md](PRODUCTION.md#ui-state-morph-brief).
- **Long-form films:** use a director's brief, style guide, storyboard/stills, animatic, full pass, polish, audio, then final render. Divide chapters only after a shared `ANIMATION_GUIDE.md` defines visual primitives, timing, asset ownership, and render contract.
- **Generate then trace:** a generated clip may inform motion or physics, but the final code layer must have a deliberately consistent visual identity and lawful asset use. Treat generated footage as a reference or disposable base, not proof of ownership.

## Client handoff

For a client film, agree on the factual brief, final formats, included revision rounds, and ownership/licensing of every supplied or generated asset before production. A revision changes the shot list, timeline, and affected review artifacts; it is not an unreviewed export tweak. Deliver the approved masters and source only through the agreed channel.

## Completion criteria

Do not stop at source code or a first render. A film is complete only when the final media has been rendered through the selected production route, inspected with the required review artifacts, and the delivered formats match the timeline and requested output contract.
