# Captions, safe zones and automated QA

## Caption chunks
The caption is the narration, cut into chunks.
- **Size:** 1–5 words, usually 2–4. Break where a speaker breathes, never inside a grammatical construct (an article with its noun, a negation with its verb).
- **One chunk on screen at a time.** It replaces the previous one; it never accumulates. A chunk lasts at least 0.6 s. Without a voiceover, time at about 2.4 words per second; with one, time to the audio.
- **One emphasis per chunk, at most**, on the word carrying the surprise or the stake:
  - bold: the default emphasis
  - marker highlight: a named term, law, quote or name to remember (at most 2 per section)
  - accent colour marker: the answer to the big question, once per video
  - coloured word: on dark fields instead of bold
- **Numbers** use one digit system (Western digits by default) and are usually the emphasis of their chunk.
- The script line is the source of truth. Chunks split it; they never reword it.
- In `script.md`, write chunks separated by ` / ` with emphasis in `**double asterisks**`.
- **Right-to-left languages:** wrap the whole word in the emphasis tag, including attached letters, or letter joining breaks. Use the stretch character (tatweel) at most once per section.

## Safe zones (9:16, 1080×1920)
No copy above y 260, below y 1480, or at x > 940 below y 1000 (platform UI and the button column). Images may run under the UI; text may not. Titles for profile grids must also survive a 3:4 centre crop.

## Annotations on MEDIA (at most 2 per shot)
A big number with a unit line, a pin (dot with label), a name tag, a ring around a detail, a marker sweep over a document line. The marker sits above the paper and under the text.

## Automated QA checklist (zero tokens)
If the project has a lint script, run it after each scene. If not, check the same list by hand or with a short script. Each failure is one line.
- [ ] Header present; card within bounds; caption not on the card (except MEDIA `top`)
- [ ] Props inside the card; nothing in the safe-zone margins
- [ ] No wipes, fades or push-ins between scenes
- [ ] Chunk length ≤ 5 words, ≥ 0.6 s; at most one emphasis per chunk
- [ ] No glow, neon, bloom, coloured shadow or gradient orb
- [ ] One colour wash per MOTION scene; field changes only at section changes
- [ ] No console errors; no missing clip frames
- [ ] No third-party logo visible; no invented numbers, quotes or documents
- [ ] Every MEDIA asset has a row in `broll.md` with source and licence

## Optional critic
Only on request, or when automated checks are clean but the user reports a visual problem. Limited to what checks cannot see: invented numbers, broken text shaping, third-party logos, generic stock shots. The critic never approves its own author's work.
