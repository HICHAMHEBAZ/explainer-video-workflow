---
name: explainer-video-workflow
description: Interview-driven workflow for short vertical (9:16) explainer videos that mix real b-roll with motion graphics (Reels, Shorts, TikTok, LinkedIn). Use when the user wants to make an explainer video, a script plus shot list, a "media vs motion" plan, or asks for a video production workflow. It first asks about the user's references and their script and content type, then generates a tailored step-by-step workflow, a script scaffold, a b-roll log and a style file in their project.
---

# Explainer video workflow

Turns "I want a 60-second explainer about X" into a repeatable run: **interview → tailored workflow → script with a retention loop → b-roll sourcing → build → QA → two approval gates → learning**.

Derived from a production workflow used for a Moroccan-Darija explainer series. Language, brand and renderer are all variables here, not assumptions.

## Step 0. Interview (always first, never skip)

Ask with `AskUserQuestion`. Two rounds, at most 4 questions each. Skip any question the user already answered in their message. The full question bank, option labels and how each answer maps to a workflow variable are in `references/interview.md`. Read it before asking.

**Round 1, the creative inputs**
1. **References.** What should this video look and feel like? (own channel/past videos, other creators' videos, a brand kit, screenshots, nothing yet.) Follow up in plain chat for the actual links or paths. Do not fetch or download anything yet.
2. **Content source.** Article/URL, pasted text, a topic to research, or raw footage/notes.
3. **Script type.** Explainer (how/why), news breakdown, story/case study, myth-buster, tutorial, product or pitch, opinion.
4. **Language and voice.** Language or dialect, tone, on-screen caption language, whether a voiceover exists.

**Round 2, production inputs**
5. **Format.** Platform, length (default 60 s, about 15 beats), aspect ratio (default 9:16).
6. **Renderer.** What turns scenes into video: HTML pages rendered with a headless browser plus ffmpeg, Remotion, a manual editor (CapCut, Premiere, DaVinci), or "plan only, no rendering".
7. **b-roll policy.** Own footage only, free-licence archives, stock, or screenshots of public sources for commentary. This sets the rights rules.
8. **Gates.** Normal (stop at Gate A, the plan, and Gate B, the final cut) or auto (stop only at Gate B).

If a reference is a link or file, ask the user to say in one line what to copy from it (frame, captions, pacing, colours, b-roll style) and what not to copy (logos, titles, footage). Never reuse another creator's footage, logos or branding.

## Step 1. Generate the project files

Create `video-workflow/` in the current project (or the folder the user names) from `templates/`, replacing every `{{PLACEHOLDER}}` with interview answers. Never leave a placeholder unfilled: use a stated default or ask.

| File | Source template | Purpose |
|---|---|---|
| `video-workflow/WORKFLOW.md` | `templates/workflow.template.md` | The tailored run order, read map, gates, QA, learning. **This is the deliverable.** |
| `video-workflow/style-preferences.md` | `templates/style-preferences.template.md` | Brand and reference notes plus "current defaults", updated after every run. |
| `video-workflow/BRIEF.md` | `templates/worker-brief.template.md` | Fixed brief for scene builders (subagents or the user's editor). |
| `runs/<run-id>/script.md` | `templates/script.template.md` | Created at the start of each run, not now. |
| `runs/<run-id>/broll.md` | `templates/broll-log.template.md` | Created during sourcing. |

Placeholders the interview does not ask directly (`SERIES_NAME`, `FONTS`, `PALETTE`, `MASCOT`, `DATE`, `AUTO_NOTE`, `BUILD_NOTE`, `SKIPPED_STEPS_NOTE`, `EXTRA_DEFAULTS`) come from the references the user gave, from one plain-chat follow-up ("series name, fonts, colours, mascot?"), or from a stated default (system-safe open fonts, a palette proposed from the references, no mascot). `BEATS` and `WORDS` follow the format answer; `AUTO_NOTE` says whether Gate A is skipped; `SKIPPED_STEPS_NOTE` lists steps dropped by the renderer choice.

Steps in `WORKFLOW.md` come from `references/workflow-steps.md`. Drop the steps the renderer choice makes irrelevant (for example no render queue for "plan only") and say so in the file.

## Step 2. Show the user the workflow

Reply with a compact table of the steps (number, name, who does it, output, stop or not) and the three or four choices that shaped it. Then ask one question: start a run now (needs the content source) or adjust the workflow first.

## Step 3. Running a video

Follow `video-workflow/WORKFLOW.md` exactly. Read only the reference files a step names (the read map is in that file). In short:

1. **Script**: `references/script-loop.md` (stakes, big question, head fakes, rehooks) and `references/captions.md`.
2. **Route each beat** MEDIA or MOTION: `references/media-vs-motion.md`.
3. **Source b-roll** and log every asset: `references/sourcing-rights.md`.
4. **Gate A**: show the script table, shots and looks. Build nothing in normal mode until the user approves.
5. **Build, QA, assemble**, then **Gate B**: final cut.
6. **Learning**: `references/learning-loop.md`.

## Hard rules (apply in every run)

- **Never invent** numbers, quotes, receipts, documents, UI or logos. A missing source turns the beat into an illustration (MOTION), never a fake MEDIA shot.
- **Rights are the user's call.** Never approve, permit or declare rights on the user's behalf. For social or web content, wait until the user states a rights declaration in chat and record their exact words.
- **Never self-approve.** Quality checks are separate from authoring; the user approves the two gates.
- **Safe zones** for 9:16: keep copy out of the top 13%, the bottom 23% and the right-hand button column (details in `references/captions.md`).
- **Spend tokens on thinking, not on images.** Review contact sheets, not loose frames. Keep command output short.
- Do not download files or publish anything without the user's yes.
