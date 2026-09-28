# Review, Correction, and Delivery

A render is evidence only after it has been watched at the sizes and moments where motion design fails.

## Required review artifacts

Generate these from the current render using the project's media tooling:

- **Contact sheet:** representative frames across the full film; use roughly two frames per second for short films, arranged in reading order. It reveals cadence, shot variety, and compositional drift.
- **Action strip:** 8–12 consecutive frames around each fast transform, text swap, UI interaction, or cut. It reveals pops, overlaps, sliding, and accidental frame-to-frame discontinuities.
- **Phone sheet:** frames scaled to 360 px wide. It verifies reading order, copy size, and image hierarchy where most short-form films are consumed.
- **Loop check:** if looping was requested, play the output at least twice continuously and inspect the seam at speed.
- **Determinism check:** render a chosen frame or identical short range twice and compare checksums/pixels. A mismatch is a render-contract defect, not cosmetic variance.

For longer films, produce contact sheets by chapter plus strips at every chapter boundary and high-motion transition.

## Critique pass

Open the artifacts. Assess them as a critical motion director, not as the implementation author. Score each dimension 1–10 with timestamps and concrete evidence:

1. Hook in the first two seconds.
2. Readability at phone size.
3. Motion quality: physical acceleration/deceleration, no dead or unintentionally sliding frames.
4. Variety and pacing: a visible development every 2–4 seconds (3–5 seconds for deliberate long-form beats).
5. Composition, depth, and visual hierarchy.
6. Brand/source accuracy and copy correctness.
7. Sound synchronization and causal SFX.

Log the scores, timestamps, three worst problems, change made, and follow-up score in `docs/review_log.md`. Target 8+ for every applicable dimension. Correct the three worst verified problems, rerender affected ranges when the renderer can do so without changing boundary frames, then regenerate the relevant review artifacts. Repeat. A flagship/high-polish film requires at least three substantive passes; a shorter piece continues until its applicable scores meet the threshold or the user explicitly accepts a documented tradeoff.

Hunt actively for these defects:

- copy collision, clipping, or a swap that exposes both labels;
- typography blurred by scaling a composited layer or camera transform;
- a generic centered title/fade, unmotivated corner label/border, glow, or decorative burst;
- motion that linearly slides, bounces without character reason, or stops on an empty beat;
- visual content that disagrees with a real product asset, metric, or brand system;
- a beat/click with no visual cause—or a consequential visual moment with no audible support;
- loop geometry, cursor, velocity, or sound discontinuity;
- non-deterministic frame output.

Correct the system cause: update the timeline, layout, motion primitive, asset, or sound cue. Do not mask a defect with a one-frame patch, lowered quality bar, or a special-case input.

## Final delivery checklist

Before delivery, verify:

- Final MP4 plays at each requested size/aspect ratio, with the agreed codec/pixel format and synchronized audio.
- Every format was laid out from the shared semantic timeline, not cropped blindly from another format.
- `out/final.mp4`, a poster frame, contact sheet, and required loop check exist; source files and production records remain reproducible.
- Product assets and claims have traceable sources; audio, voice, and reference use honor permissions.
- `docs/style_guide.md`, `docs/shotlist.md`, and `docs/review_log.md` exist whenever their applicable gates were used.

Report the rendered files, formats, final scores, sources/assumptions, and residual constraints. Never describe a final render or visual review that did not happen.
