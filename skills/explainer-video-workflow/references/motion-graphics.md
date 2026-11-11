# Motion graphics system

Used by the graphics workers once `words.json` is final. Look tokens (palette, fonts) come from `style-preferences.md`; the grammar below is fixed. Routing between footage and graphics: `media-vs-motion.md`.

## When a graphic is required, optional, forbidden
- **Required:** a statistic that is the point of its sentence (count-up); two or more numbers compared (bars); two or more dates in sequence (date ruler); a mechanism or aggregate with no filmable referent (collage); a group of named people with no shared footage (portrait grid); where / how far / a route (map).
- **Optional:** the kinetic key word; a number that already has a document page (prefer the page).
- **Forbidden:** over the first 1.5 s of a speaker's sound bite; on deaths or accidents (only a grey date chip); decoration that carries no fact; more than 2 graphics in a row; a graphic replacing footage of the very event unless the sentence carries a number; drawn faces of real people (real photo cut-outs of public figures allowed, private people never); outlet logos; glow, neon, gradient orbs.
- **Share:** 20–35 % of runtime, at least 3 per video, at least 1 every 30 s.

## Grammar (tokens come from the style file)
| Element | Spec |
|---|---|
| Field | one flat background colour with optional static grain; one colour wash per graphic scene |
| Number | large serif or display face, count-up 0.8–1.2 s ease-out starting on the spoken digit; unit smaller, after the number |
| Bars | grow from a baseline over 0.6 s; at most 4; a dashed ghost bar for "before" or "projected"; label above |
| Accent | **one** accent colour per shot (the subject bar or the underline); one highlight marker colour behind a label |
| Cut-outs | subject cut from a photo, flat paper edge, hard offset shadow (no blur); faces stay in colour |
| Plaques | 1–3 words beside or under an object, never sentences |
| Layouts | `row` (2–4 objects) · `ride` (objects on a carrier) · `stack` · `equation` (A + B = C) · `grid` (portraits) · `chalk` (geometric mechanism, at most 1 per video) · `custom` (a worker builds it, at most 3 per video) |

## Entrances (this is the motion)
- Step by step **on the spoken words**: nothing appears before its word. Objects pop (scale 0.85→1, 0.25 s, back ease); lines draw 0.5–0.8 s; one new element every 0.4–1.0 s; the last 0.4 s is still.
- Over footage: at most one mark per shot, at most one accent colour on screen, marks stay inside the safe zone and out of the caption slot.
- New element every 2.5–4 s across the video (a small mark, not a new scene).

## Worker protocol
- One message per worker with everything: scene folder, the per-scene block (see `BRIEF.md`), paths to `words.json` and the caption chunks with their times, and the literal rule: **the scene file must contain `window.DURATION = <seconds>;` as a plain number** (a computed or missing value breaks assembly).
- Workers write only in their own scene folder, never source or download, never edit another scene, never render video. They check with **stills** (middle and end frames) and the project lint, then report in five lines.
- Custom graphic scenes are locked after they pass (a `custom.lock` marker or equivalent) so a rebuild never overwrites them.
- Max 3 workers at once. Use a small, cheap model for workers and keep the strongest model for script, routing and fixes.
- Graphic text is data, never the caption again. One focal object, readable in under 2 s at phone size.

## Aspect ratio
Positions in `BRIEF.md` are written for 9:16. For another ratio, scale the content band and safe zones using the table in `captions.md`, and for 16:9 prefer wider layouts (`row`, `equation`, map) over tall stacks.
