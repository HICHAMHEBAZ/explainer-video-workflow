# Captions, safe zones and automated QA

## Caption chunks
The caption is the narration, cut into chunks.
- **Size:** 1–5 words, usually 2–4 (at most 2 lines, 4 words a line). Break where a speaker breathes, never inside a grammatical construct (an article with its noun, a negation with its verb).
- **One chunk on screen at a time.** It replaces the previous one; it never accumulates. A chunk stays at least 0.6 s. With a voiceover time chunks to `words.json`; without one, about 2.4 words per second.
- **One emphasis per chunk, at most**, on the word carrying the surprise or the stake: bold (default), marker highlight (a named term, law, quote or name; at most 2 per section), accent colour (the answer to the big question, once per video), coloured word on dark fields.
- **Numbers** use one digit system (Western digits by default) and are usually the emphasis of their chunk.
- The script line is the source of truth. Chunks split it; they never reword it.
- In `script.md`, write chunks separated by ` / ` with emphasis in `**double asterisks**`.
- **Right-to-left languages:** wrap the whole word in the emphasis tag, including attached letters, or letter joining breaks. Use the stretch character (tatweel) at most once per section. Do not end a line on a short connector word that belongs to the next word.

## Canvas and safe zones by aspect ratio
Text stays inside the safe area; images may run under platform UI.

| Ratio | Canvas | No copy in | Notes |
|---|---|---|---|
| 9:16 | 1080×1920 | top 13 % (y < 260), bottom 23 % (y > 1480), right column (x > 940 below y 1000) | caption slot sits low-middle (about y 1150–1400); content band y 330–1280; profile-grid titles must survive a 3:4 centre crop |
| 4:5 | 1080×1350 | top 8 % (y < 110), bottom 12 % (y > 1190), 6 % side margins (x < 65 or x > 1015) | caption slot about y 880–1100 |
| 1:1 | 1080×1080 | 8 % margin on every side (88 px) | caption slot about y 760–900; keep key detail out of the corners |
| 16:9 | 1920×1080 | 5 % margins (x < 96 or x > 1824; y < 54 or y > 1026); bottom 15 % reserved for platform controls | caption slot lower third about y 780–900; wider layouts, two-line captions up to 6 words a line |

If the user's platform or references disagree with the table, the user's numbers win; record them in `style-preferences.md`.

## Annotations on MEDIA (at most 2 per shot)
A big number with a unit line, a pin (dot with label), a name tag, a ring around a detail, a marker sweep over a document line. The marker sits above the paper and under the text.

## Automated QA checklist (zero tokens)
If the project has a lint script, run it after the build. If not, check the same list by hand or with a short script. Each failure is one line.
- [ ] Header present; content inside the band; caption not on the content (except MEDIA `top`)
- [ ] Nothing in the safe-zone margins for the chosen ratio
- [ ] Hard cuts only (no wipes, fades or push-ins between scenes)
- [ ] Chunk length ≤ 5 words, ≥ 0.6 s; at most one emphasis per chunk
- [ ] No glow, neon, bloom, coloured shadow or gradient orb
- [ ] One colour wash per graphic scene; field changes only at section changes
- [ ] No console errors; no missing clip frames; each graphic scene declares a literal duration
- [ ] No third-party logo visible; no invented numbers, quotes or documents
- [ ] Every MEDIA asset has a row in `broll.md` with source and licence
- [ ] Shot-list limits from `footage-and-sourcing.md` §5 hold

## Optional critic
Only on request, or when automated checks are clean but the user reports a visual problem. Limited to what checks cannot see: invented numbers, broken text shaping, third-party logos, generic stock shots, wrong-event footage. The critic never approves its own author's work.
