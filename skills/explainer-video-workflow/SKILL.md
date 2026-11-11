---
name: explainer-video-workflow
description: Intake-first, voice-first workflow for short explainer videos (Reels, Shorts, TikTok, LinkedIn) that mix real b-roll with motion graphics. Use when the user wants to make an explainer, a reel, a short, a script plus shot list, a voiceover-to-video pipeline, or asks for a video production workflow. It first asks for the user's references, how they write, and the aspect ratio; then writes a tailored workflow and runs it end to end: script, voice chain, footage scout, b-roll sourcing, motion graphics, build, QA, hand-off.
---

# Explainer video workflow

Turns "I want an explainer about X" into a repeatable run:

**intake (references, writing style, aspect ratio) → tailored workflow → script → footage scout → Gate A → voice → voice chain → b-roll + motion graphics in parallel → build → QA → Gate B → post package → learning**

Distilled from a production workflow for a Moroccan-Darija explainer series. Language, brand, writing style, aspect ratio and renderer are variables here, never assumptions.

## Step 0. Intake (always first, never skip)

Use `AskUserQuestion`. The three creative questions come first, in this order, in one round. Skip any the user already answered. The full bank, option labels and how each answer becomes a variable are in `references/interview.md`. Read it before asking.

**Round 1, the creative inputs (ask these before anything else)**
1. **References.** What should this look, sound and feel like? Own channel or past videos, other creators (inspiration only), a brand kit, screenshots, nothing yet. Then ask in plain chat for the links or paths and one line: what to copy, what not to copy. Fetch nothing yet.
2. **How you write.** Your script voice: sample scripts or captions, the viewer you write to, register and dialect, sentence length, how you open, words you avoid, person (I / you / we), report vs opinion. Details: `references/writing-style.md`.
3. **Aspect ratio and format.** 9:16, 4:5, 1:1 or 16:9; length; platforms. The ratio sets canvas, safe zones and caption layout (`references/captions.md`).

**Round 2, production inputs**
4. **Content source and script type** (URL, pasted text, topic to research, own footage; explainer, news breakdown, story, myth-buster, other).
5. **Voice.** I record it myself, AI voice, supplied audio, or captions only; language or dialect.
6. **Renderer.** HTML pages + headless browser + ffmpeg, Remotion, a manual editor, or plan only.
7. **b-roll policy and rights.** Own footage, free licences, stock, YouTube or social clips (the user states the rights declaration), screenshots for commentary.
8. **Gates.** Normal (stop at the script, then the cut) or auto (stop only at the cut).

Echo the answers back in six lines before writing files. If a reference is a link or file, never reuse another creator's footage, logos or branding.

## Step 1. Generate the project files

Create `video-workflow/` in the current project (or the folder the user names) from `templates/`, replacing every `{{PLACEHOLDER}}`. Never leave one unfilled: use a stated default or ask.

| File | Source template | Purpose |
|---|---|---|
| `video-workflow/WORKFLOW.md` | `templates/workflow.template.md` | The tailored run order, read map, gates, QA. **The deliverable.** |
| `video-workflow/style-preferences.md` | `templates/style-preferences.template.md` | Brand, references, **writing style**, aspect ratio, defaults that learn from each run. |
| `video-workflow/BRIEF.md` | `templates/worker-brief.template.md` | Fixed brief for scene builders (subagents or the user's editor). |
| `runs/<run-id>/script.md` | `templates/script.template.md` | Created at the start of each run. |
| `runs/<run-id>/broll.md` | `templates/broll-log.template.md` | Created during sourcing. |

`SAFE_ZONES` is the row of the chosen ratio in `references/captions.md`; `VIEWER`, `REGISTER`, `RHYTHM`, `TONE`, `STANCE`, `AVOID_WORDS` come from the writing-style answers.

Steps in `WORKFLOW.md` come from `references/workflow-steps.md`. Drop the steps the renderer or voice choice makes irrelevant and say so in the file.

## Step 2. Show the user the workflow

Reply with a compact table (step, who, output, stop or not) and the three or four choices that shaped it. Then ask one question: start a run now (needs the content source) or adjust first.

## Step 3. Running a video

Follow `video-workflow/WORKFLOW.md` exactly. Read only the reference files a step names.

| Stage | What happens | Read |
|---|---|---|
| Script | Written in the user's style, delivered as numbered chunks `S01…` of one or two sentences | `writing-style.md`, `script-loop.md`, `captions.md` |
| Footage scout | Search only, no downloads: what is really filmable for each named thing | `footage-and-sourcing.md` |
| **Gate A** | User reads the chunks and the `visual:` plan, then records | |
| Voice | Transcribe first, compare with the script, fix from what was said | `voice-chain.md` |
| Voice chain | Pick takes, align word timings, denoise, trim dead air, audit; `words.json` is final | `voice-chain.md` |
| Workers | b-roll download + cut check and motion-graphics scene builders start together, max 3 in parallel | `footage-and-sourcing.md`, `motion-graphics.md`, `media-vs-motion.md` |
| Build, QA | Shot list, scenes, lint, one contact sheet | `captions.md` |
| **Gate B** | Preview or editor hand-off; export only when the user says "export" | |
| Post, learning | Post package, credits, retro, defaults updated | `learning-loop.md` |

## Hard rules (every run)

- **Never invent** numbers, quotes, receipts, documents, UI or logos. A missing source turns the beat into an illustration, never a fake MEDIA shot.
- **Footage shows the named thing; graphics explain concepts.** A wrong-event or wrong-year clip is a factual error, not a rights question.
- **Rights are the user's call.** Never approve or declare rights for them; record their exact words.
- **Never self-approve.** Builders build, checks and the user review.
- **Voice first.** The recorded voice is the truth: if it deviates from the script, fix captions from what was said (or flag a re-record), then build.
- **One fix, then flag.** Read a failing command's error once, fix the cause once; if it fails again take the fallback or drop the item and name it in the hand-off. No retry loops. Never pipe a chain tool through grep/head/tail (it swallows errors).
- **Nothing from memory.** No URL, number, name, clip range or file name that is not in the research file, the script, the shot list, the scout file or a tool's output.
- **Safe zones** come from the chosen aspect ratio (`captions.md`).
- **Spend tokens on thinking, not images.** Contact sheets, not loose frames; short command output.
- No downloads, publishing or export without the user's yes.
