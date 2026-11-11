# Workflow steps (source of truth for WORKFLOW.md)

Two stops: **Gate A** (script chunks and visual plan, before the user records) and **Gate B** (final cut). In auto mode only Gate B stops. Never build from a Gate A that is not approved (normal mode).

## Roles
- **Orchestrator** (the main session, strongest model): script, routing, sourcing, short briefs, fixes, assembly.
- **Writer review**: a separate reviewer checks the script before the user sees it.
- **Workers** (cheap-model subagents, or the user's editor): scene builders and a footage-search scout. About 3 scenes each, one message each.
- **QA**: automated checks first, then one contact sheet. A model critic only on request. Whoever wrote a scene never approves it.

## Read map
| Step | Orchestrator reads | Workers read |
|---|---|---|
| 0 Preflight | `style-preferences.md`, `media-vs-motion.md` | |
| 1 Script | `writing-style.md`, `script-loop.md`, `captions.md` | |
| 2 Scout | `footage-and-sourcing.md` | |
| 4-5 Voice | `voice-chain.md` | |
| 6 Workers | `footage-and-sourcing.md`, `motion-graphics.md`, `BRIEF.md` | `BRIEF.md` |
| 8 QA | contact sheet only | |
| 11 Learning | `learning-loop.md` | |

## 0. Preflight (silent)
Read the style file (references, writing style, format). Fix canvas, fps and safe zones from the aspect ratio. Check the tools exist: `ffmpeg -version`, the ASR tool, the downloader (if footage is sourced), the headless browser or Remotion. A missing tool is told to the user once with the install command; continue with steps that do not need it. For downloads that need cookies, check the access once now so a bot check does not appear at step 7.

## 1. Script
- Input: the content source. Research into `research/<slug>.md` with a URL for every on-screen fact (skip for pasted text).
- Write in the user's style (`writing-style.md`) with the loop mechanics (`script-loop.md`). Length from the format (about 2.4 spoken words per second).
- Format: numbered chunks `S01 | …` of one or two sentences, a `visual:` line (what it shows, family) and a `src:`. Save `runs/<id>/script.md`.
- A separate reviewer pass fixes facts, language rules, stance and flow.

## 2. Footage scout (parallel with step 1 once the nouns are known)
`footage-and-sourcing.md` §1: search only, `scout.md`. `visual:` lines come from AVAILABLE entries; NONE becomes a graphic.

## 3. Gate A
Deliver the script in the chat as numbered chunks plus the five-line note and the `visual:` plan. The user reads each chunk twice and records each chunk twice (or approves a TTS voice). Stop. Auto mode: skip the stop and continue as soon as a voice exists.
After approval record the user's rights words verbatim. Never write a declaration for them.

## 4. Voice, first look
`voice-chain.md`: transcribe the raw voice, compare with the script as a whole, fix script and captions from what was said or flag a re-record.

## 5. Voice chain
Pick takes, align, clean, trim dead air, audit, freeze: `voiceover-final.wav` + `words.json`. Skipped for `VO=none`.

## 6. Workers (b-roll and graphics together, max 3 in parallel)
- **b-roll** (lead, not a worker): probe three shots, download the rest, cut, run the cut check, write `credits.md` and `broll.md` (`footage-and-sourcing.md`).
- **Graphics** (scene builders): graphic scenes per `motion-graphics.md`, one message per worker, literal `window.DURATION`.
- Independent steps (music search, shot list prep) run in the third slot.

## 7. Shot list and build
Fill the shot list from the script, `words.json` and the cut files (rules in `footage-and-sourcing.md` §5); validate it (ranges inside the footage, chunk lengths, share limits). Build every scene from it. Footage scenes use the cut files; graphic scenes come from the workers. Captions use the script spelling with chunk times from `words.json`.

## 8. QA
1. Automated checks after the build (`captions.md` checklist): safe zones, chunk length and emphasis, flat materials, console errors, missing frames, shot-list limits. One failure per line; fix and re-run once.
2. One contact strip of the whole cut (a frame every 1.5 s); the orchestrator opens it once.
3. Optional critic on request, limited to what checks cannot see: invented numbers, wrong-event footage, third-party logos.

## 9. Music and sound
2–4 music cues from a licensed or user-supplied library; one cue per section, ducked under the voice (about -18 dB under speech). Sound effects only on about 40–50 % of cuts, never on sensitive topics.

## 10. Gate B: hand-off
Show the preview (or the editor project) and the contact strip, with a short message: length, shots that fell back to graphics for lack of footage, reused pictures, shots under 2 s, uncertain phrases, weak sources. The user trims in the preview or sends notes. **Export only when the user says "export"**; then render in the background and report the path, duration and size.

## 11. Post package and learning
- `post.md`: hook-first caption, two or three fact lines, one question plus a save/comment ask, 8–10 hashtags in three layers (brand, topic, reach), cover timecode, no source lines on screen. Platform variants: Shorts title under 100 characters; LinkedIn hook as first line with 3–5 hashtags. Never claim a tag "goes viral". Native-speaker note for dialect copy.
- `credits.md` complete.
- Learning: `learning-loop.md`.

## Speed and cost rules
- Check with stills, render once, one scene at a time on small machines.
- Cache assembled segments; re-encode only changed clips.
- Brief = "Read BRIEF.md" + per-scene blocks. Never paste document text into a brief.
- Never pipe a chain tool through `grep`/`head`/`tail`; read its summary line. One fix, then flag.
