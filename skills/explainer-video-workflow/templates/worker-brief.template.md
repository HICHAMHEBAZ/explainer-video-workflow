# Builder brief (fixed part)

The orchestrator sends each builder: "Read `video-workflow/BRIEF.md`, then build these scenes:" followed only by the per-scene block. Everything that never changes lives here. Positions below are for {{ASPECT}} ({{CANVAS}}).

## Per-scene block (the orchestrator writes this, nothing more)
```
scene: scenes/<run-id>-<nn>-<name>/        mode: MOTION | MEDIA
type: <hook | equation | map | balance | bignum | document | timeline | collage | end card>
start from: <template or picked variant>
dur: <seconds>   (write literally: window.DURATION = <seconds>;)
chunks: <caption chunks with / and **emphasis**>   at: <start time of each chunk from words.json, locked>
field/wash: <colour>   (MEDIA: layout top|low|short, asset <path>)
idea: <one line: the focal object and its one key motion; entrances on the chunk words, never before the word is spoken>
note from the card: <user note or none>
```

## Fixed rules
1. Write only in your own scene folder. Captions go in the captions file, exactly the chunks given; never reword, never add numbers, names or quotes.
2. Layout: field, header, caption, one focal object. Safe zones for this ratio: {{SAFE_ZONES}}. Props stay inside the content band. Hard cuts only.
3. Flat materials: no glow, neon, bloom, coloured shadow, gradient orb, glass. Fonts from the project font folder.
4. Graphic text is data, never the caption again. One focal object, readable in under 2 s at phone size.
5. Time each reveal to the word that says it. Entrance 0–1.2 s (focal object visible by 0.5 s), key motion, still hold of at least 0.4 s at the end. Labels never sit on top of marks.
6. The scene file contains `window.DURATION = <seconds>;` as a plain number.
7. Never source, download or edit another scene. Check with **stills only** (middle and end frames) and run the project's checks; fix every failure. Never render videos. Report back in at most 5 lines: files written, anything you could not do.

## Current defaults (copy updates from `style-preferences.md`)
- Metaphor objects for mechanism and stakes; countable units for comparisons; no plain bars.
- Ghost or dashed "before" next to a solid "after"; things physically move.
- Receipts: push-in and ring on the exact figure.
{{EXTRA_DEFAULTS}}
