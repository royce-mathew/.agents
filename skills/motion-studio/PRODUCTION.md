# Production Briefs

Use these structures as planning tools. Replace every bracketed field with source-backed information; remove irrelevant sections instead of leaving placeholders in a live brief.

## Reference-led direction

A reference supplies **grammar**, never copied subject matter.

1. For a video reference, extract a representative frame every 0.5 seconds; for a still or library, group frames by recurring visual traits.
2. Record the visual grammar in `docs/style_guide.md`:
   - palette as usable colors and their roles;
   - type family, weight, scale hierarchy, tracking, and line treatment;
   - shot duration, cut cadence, transition vocabulary, and camera behavior;
   - texture, grain, illustration rules, and negative space;
   - what is excluded: marks, characters, logo treatment, narrative content, or motifs that belong to the source.
3. Translate it into an original `docs/shotlist.md`. The reference controls the film's design language, not its product claims or story.

A style name can establish a direction, but a frame or library resolves far more: hierarchy, pacing, and transition behavior. Let the chosen renderer follow the required visual outcome unless a project framework is an actual reuse constraint.

## Product-film brief

Use for a launch film, motion ad, or branded feature reel.

```text
Product: [name] — [URL]
Audience and outcome: [who should believe or do what]
Duration / primary format / variants: [e.g. 20 s / 9:16 / 1:1 and 16:9]

Truth sources
- Capture and use actual product screens, logo, colors, and licensed fonts from [sources].
- Exact feature claims: [claim + proof source].
- Metric: [number + source + required qualifier].
- CTA: [exact final copy and destination].

Direction
- Reference: [path/link]. Borrow [palette/type/cadence/etc.]; exclude [source-specific content].
- Visual system: [background, typography, one accent, texture, camera language].
- Sound: [supplied track | synth], [tempo/character], [voice rules if any].

Beat story
1. 0:00–[t] Hook: [five-word problem or striking outcome].
2. [t]–[t] Product enters: [real UI assembles/reframes].
3. [t]–[t] Features: [three real interactions; one UI moment each].
4. [t]–[t] Proof: [the stated metric in context].
5. [t]–end Lockup and CTA: [brand end state].
```

Store all captured assets and list their origin. When authentication prevents a real capture, use supplied authenticated captures or pause that sequence; never approximate the interface from memory.

## UI state-morph brief

Use when a single UI element tells the story by changing state.

```text
Inputs
- Product / URL and real source data: [values, labels, screens].
- States (8–12): [button → email entry → loader → success → dashboard → chart → tooltip → command palette → toast → logo].
- Brand system: [colors, fonts, one accent].
- Audio and formats: [track/synth, BPM, 9:16/1:1/16:9].

Direction
One recognisable container persists across the whole film. Its size, radius, fill,
and internal layout transform; a cursor performs each consequential interaction.
A warm neutral canvas and one accent support legibility. UI motion is controlled
and physical, with at most a slight overshoot.

Beat grid
[measured or selected BPM]. Every beat advances, confirms, or recontextualizes a
state. Downbeats carry the largest state or camera changes. Final state restores
initial geometry and cursor trajectory when the output loops.
```

Build a state table before code: state, source data, entry trigger, container geometry, content layering, cursor action, beat, SFX, and exit condition. That table is the source of truth; a fake interface is a film set whose every visible value is known.

## Director's brief

Use for a flagship or long-form film. Treat it as a multi-session production, not a request for instant final media.

```text
Film in one line
[logline and the exact emotional/narrative payoff]

Inputs and rights
- References: [video, frames, image library, prior project]. Keep [grammar]; exclude [content].
- Audio: [path + whether unchanged] or [score brief].
- Tools: [existing renderer/skills/APIs], credentials only through environment variables.
- Budget / runtime: [limit]. Use paid tools deliberately.

Look and identity
[palette, type, texture, camera language, character proportions/expressions if applicable]
[identity locks that must survive every scene]

Beat sheet
0:00–0:02 [single striking hook]
0:02–[t] [act / visual payoff]
... [a new payoff every 3–5 seconds]
[end] [resolves to or sets up the first frame when looping]

On-screen language
[when copy, captions, or lyrics dominate; safe composition zones; accessibility/copy constraints]

Deliverables
[formats, final media, poster, contact sheet, loop check, source]
```

Create the style guide and detailed shot list; build stills for every shot; make a low-resolution animatic with placeholder audio; fix story and pacing; then animate, polish, score, review, and render. For parallel chapters, `docs/ANIMATION_GUIDE.md` must define shared timing, primitives, asset boundaries, naming, and quality thresholds before work divides.
