# Deterministic Render Engine

The renderer must answer: “What does the frame at time `t` look like?” without first visiting any earlier frame. This makes frame-level revisions, subframe motion blur, rerenders, and determinism checks reliable.

## Render contract

For a seek renderer, expose `window.seek(t)` and make it paint the complete frame for time `t`.

- Clear and redraw the full scene on every seek. Derive all scene choice, geometry, opacity, camera, cursor, particles, and texture from `t`, timeline data, and fixed seeds.
- In capture mode, exclude `requestAnimationFrame`, CSS/WAAPI transitions, timers, delayed asset loading, persistent mutable animation state, and `Math.random`. A normal-browser preview may use a clock only to call the same pure draw function.
- Use local assets and await fonts before capture. Canvas text or DOM layout rendered before fonts load invalidates visual review.
- Do not apply `will-change`/layer promotion to text or UI that the camera scales; render it at its final apparent scale or use a composition that preserves sharp type.
- Render the frame sequence with a headless browser or the selected framework's deterministic renderer. Encode H.264 with `yuv420p` compatibility; target CRF 16 unless the project has an established delivery spec.
- Default to 60 fps. For fast motion, capture four evenly spaced subframes per output frame and blend them into motion blur. Do not merely duplicate frames.

Keep timeline data separate from drawing primitives: scenes, state changes, beats, copy, and sound cues belong in inspectable data. A layout function maps semantic regions to each output aspect ratio, so 9:16, 1:1, and 16:9 share narrative timing but can recompose safely.

## Physical motion

Use closed-form damped springs, evaluated directly at elapsed time. A spring is deterministic and has perceived mass; arbitrary easing curves often look like slides.

- **Snappy:** controls, toggles, leading edges.
- **Default:** cards, containers, camera.
- **Heavy:** large type, large objects, end lockups.
- **Playful:** mascot/sticker motion; overshoot belongs only where it serves the character.

For a property with multiple targets, do not simulate or restart state. Start with the first value and add the delta for each subsequent key multiplied by a spring that begins at that key's time:

```js
function track(t, keys, spring) {
  let value = keys[0].value;
  for (let i = 1; i < keys.length; i++) {
    value += (keys[i].value - keys[i - 1].value) * spring(t - keys[i].time);
  }
  return value;
}
```

This keeps motion continuous while allowing any isolated frame to be rendered. For stretching indicators or elastic tabs, evaluate leading and trailing edges with different spring stiffness. For a morphing container, start new content after the geometry begins changing and remove old content before the next state begins.

Use seeded noise for texture or particle placement. Choose a fixed seed per scene/entity; consuming a shared mutable random stream makes output order-dependent.

## Beat and sound contract

Sound determines edit timing; it is not a final overlay.

1. **Supplied track:** analyze the source before animation. Persist measured BPM, beat times, downbeats, and onset peaks in `beats.json`. Align state changes/cuts to beats, major transitions to downbeats, and UI hits to appropriate peaks. Respect the supplied track's license and do not alter it unless authorized.
2. **No track:** synthesize score and SFX from the same timeline. Start with a tempo such as 120 BPM only as a deliberate creative choice, then generate musical events and cues on its grid.
3. **Effects:** make clicks, pops, thumps, and whooshes directly correspond to visible cause and effect. Seed synthesized noise. Mix final program audio to roughly -14 LUFS unless the intended distribution requires another documented target.
4. **Voice:** load credentials from environment variables, keep them out of source and prompts, and obtain explicit authorization for voice identity/style.

Render video and sound separately when that keeps iteration fast, then mux/mix them without changing duration or frame alignment. Treat every cue's time as timeline data.

## Framework-specific equivalence

Frameworks may own the API, but never relax the contract:

- In **Remotion**, composition frame/time and seeded props replace browser state. Use its Studio for fast timeline inspection and renderer for final media.
- In **HTML/GSAP frameworks**, build against an explicit seekable timeline or their documented frame-render path. Capture must not depend on wall-clock animation.
- In **canvas**, a single `seek(t)` entry point plus testable drawing primitives is normally enough. Prefer a single page for a self-contained one-off; split only when reuse or a large film makes the seam valuable.
