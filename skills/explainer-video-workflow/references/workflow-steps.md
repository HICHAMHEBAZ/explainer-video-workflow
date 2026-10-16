# Workflow steps (source of truth for WORKFLOW.md)

Two stops: **Gate A** (script, shots, looks) and **Gate B** (final cut). In auto mode only Gate B stops. Never build from a Gate A that is not approved (normal mode).

## Roles
- **Orchestrator** (the main Claude session, strongest model): script, routing, sourcing, short briefs, fixes, assembly.
- **Builders** (subagents on a cheaper model, or the user's editor): build scenes from a fixed brief. About 3 scenes each, launched in one message.
- **QA**: automated checks first (a lint script or the checklist in `captions.md`), then contact sheets for the user. A model critic only on request. Whoever wrote a scene never approves it.

## Read map (read only what the step needs)
| Step | Orchestrator reads | Builders read |
|---|---|---|
| 0 Preflight | `style-preferences.md`, `media-vs-motion.md` | |
| 1 Script | `script-loop.md`, `captions.md` | |
| 2 Sourcing | `sourcing-rights.md` | |
| 3 Gate A / 4 Build | `BRIEF.md` | `BRIEF.md` |
| 5 QA | contact sheets only | |
| 8 Learning | `learning-loop.md` | |

## 0. Preflight (silent, no questions)
Read the style file. Fix the format (aspect, resolution, fps). Check the renderer's tools exist (`ffmpeg -version`, the headless browser or Remotion install). If a tool is missing, tell the user once, with the install command, and continue with the steps that do not need it.

## 1. Script and shot list
- Input: the content source. About 15 beats for 60 s, 120–140 spoken words.
- Write with the retention loop (`script-loop.md`) and run its self-check.
- Scene table per beat: time, line (as caption chunks), mode (MEDIA or MOTION) with the routing rule number, visual, loop tag, section. Under the table: **big question**, **head fakes**, **final rehook**, MEDIA/MOTION share.
- Beat 1 is the hook: the stake or question lands in the first 1.5 s.
- Last beat before the end card never feels finished: it opens a question for the comments.
- Save `runs/<run-id>/script.md`.
- Every MEDIA beat gets a **literal target** (the named person, place, document, page), a search query and a search language. No generic stock.

## 2. Source b-roll (parallel with step 3a when possible)
Follow `sourcing-rights.md`. Receipts first (real screenshot with the quoted text located), then real things from free archives, then auto-pick the top literal candidate and keep two alternates. Nothing literal found: flip the beat to MOTION and note it. Write `broll.md`.

## 3. Gate A: script, shots, looks
**3a. Looks, built before the user sees anything.** MOTION beats: 3 variants (A follows the defaults, B changes layout or unit shape, C breaks a default). MEDIA beats: 1 variant from the defaults, rebuilt only if the user picks another layout. Star one variant per beat, the one the defaults favour. Skipped for the *plan only* and *manual editor* renderers: write one visual description per beat instead.
**3b. The board.** One card per beat: caption chunks, mode badge, sourced shot with source and licence, variants with the star. Chat-only: a numbered list; the user answers "approve" or a note per number. Reset any old gate state first.
**3c. User response.** "Approve" (untouched beats take the star), or picks and notes. Only changed beats are redone.
**3d. Rights record.** After approval, record the approval and each rights declaration in the user's own words. Never before; never write a licence or declaration for the user.

## 4. Build (skip for *plan only*)
Every beat is one scene: a page, composition or editor spec, plus its captions file. Builders follow `BRIEF.md` and write only in their own scene folders. They check with **stills**, not renders. Opus runs one render queue, one scene at a time, in the background.

## 5. QA
1. Automated checks after each scene: layout, safe zones, caption chunk length and emphasis, flat materials, console errors, missing frames. One failure per line; fix and re-run until clean.
2. Contact sheet per scene (one frame every 1.5 s) for the user; the orchestrator does not open each one.
3. After assembly: one overview contact sheet of the whole cut; the orchestrator opens it once as a sanity glance.
4. Optional critic subagent on request, limited to what automated checks cannot see: invented numbers, broken text shaping, third-party logos, generic stock.

## 6. Assemble
Join scenes in order with hard cuts; add SFX, voiceover and music if present (re-time captions to the audio). Produce the video, a cover frame (the hook's end frame, title inside the 3:4 grid crop for profile grids), and the post package per platform:
- **Instagram/TikTok**: hook line, 3 short takeaways, source credit, a comment question, 10–15 hashtags.
- **Shorts**: title under 100 characters (hook + keyword), 2-line description with source credit, 3 hashtags.
- **LinkedIn**: hook as the opening line, 3 takeaways, source credit, one question, 3–5 hashtags.
Write `credits.md` listing every b-roll asset with author and licence.

## 7. Gate B: final cut
Show the video and the overview sheet. The user approves, or sends notes (the orchestrator edits the touched scenes, re-renders them, re-assembles). Optional: a local editing UI if the project has one.

## 8. Learning (unasked, when the run is done, short)
Follow `learning-loop.md`: log the picks, promote anything chosen twice to a default, record b-roll decisions, add one line to the brief for any repeated QA flag, write a 3-line retro at the end of `script.md`.

## Speed and cost rules
- Check with stills, render once. Render one scene at a time on small machines.
- Cache assembled segments; re-encode only clips whose speed changed.
- Brief = "Read BRIEF.md" + per-scene blocks. Never paste doc text into a brief.
- Pipe long logs through `tail -5`.
