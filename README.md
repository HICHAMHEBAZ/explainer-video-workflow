# explainer-video-workflow

A Claude Code skill that runs a repeatable, **voice-first** workflow for short explainer videos (Reels, Shorts, TikTok, LinkedIn) mixing real b-roll with motion graphics.

It starts by **asking you three things**: your **references**, **how you write**, and the **aspect ratio**. Then it writes a tailored `WORKFLOW.md` and runs the whole pipeline with you: script, voice recording and cleanup, footage scout, b-roll sourcing, motion graphics, build, QA, hand-off.

## What you get

```
video-workflow/
├── WORKFLOW.md            ← your tailored steps, gates, read map
├── style-preferences.md   ← brand, references, writing style, ratio, defaults that learn
└── BRIEF.md               ← fixed brief for scene builders
runs/<run-id>/
├── script.md              ← chunks S01…, visual plan, loop notes
├── scout.md               ← what is really filmable for each named thing
├── words.json             ← per-word timings from your final voice
├── broll.md · credits.md  ← every asset with source, licence, your rights words
└── post.md                ← caption, hashtags, cover frame
```

## The pipeline

| # | Step | Stop? |
|---|---|---|
| 0 | Preflight (tools, access, canvas and safe zones from your ratio) | |
| 1 | Script in **your** writing style, numbered chunks `S01…`, separate reviewer pass | |
| 2 | **Footage scout**: search only, AVAILABLE / LATER-ERA / NONE per filmable noun | |
| 3 | **Gate A**: chunks + visual plan; you read each twice and record each twice | yes |
| 4 | **Voice first**: transcribe, compare with the script, fix from what was said | |
| 5 | **Voice chain**: pick takes, align words, denoise, trim dead air, audit, freeze `words.json` | |
| 6 | **Workers in parallel (max 3)**: b-roll download + cut check ‖ motion-graphics scenes | |
| 7 | Shot list and build | |
| 8 | QA: lint, one contact strip | |
| 9 | Music and sound | |
| 10 | **Gate B**: preview hand-off; export only when you say "export" | yes |
| 11 | Post package, credits, learning (picks become defaults) | |

## Install

### Option 1: plugin marketplace (recommended)

Inside Claude Code:

```
/plugin marketplace add HICHAMHEBAZ/explainer-video-workflow
/plugin install explainer-video-workflow@explainer-video-workflow
```

### Option 2: copy the skill

```bash
git clone https://github.com/HICHAMHEBAZ/explainer-video-workflow.git
cp -r explainer-video-workflow/skills/explainer-video-workflow ~/.claude/skills/
```

For one project only, copy it to `<project>/.claude/skills/` instead. On Windows, `~/.claude` is `C:\Users\<you>\.claude`.

## Use

Say any of:

- "Make an explainer video workflow for my channel"
- "I want a 60-second Reel from this article"
- `/explainer-video-workflow`

### The intake (always first)

**Round 1, creative**
1. **References**: your past videos, other creators (inspiration only), a brand kit, screenshots, or none; what to copy and what not to copy.
2. **How you write**: sample scripts or a description (viewer, dialect, rhythm, tone, stance, words to avoid).
3. **Aspect ratio and format**: 9:16, 4:5, 1:1 or 16:9; length; platforms.

**Round 2, production**: content source and script type · voice (you record, AI, supplied audio, captions only) · renderer (HTML + ffmpeg, Remotion, manual editor, plan only) · b-roll policy and rights · gates.

## Principles baked in

- **Voice first.** The recorded voice is the truth; captions and cuts follow it.
- Footage shows the named thing, graphics explain concepts. Nothing honest to film becomes a graphic.
- Never invent numbers, quotes, receipts or logos.
- You own the rights decisions. Claude never approves or declares rights for you.
- Nobody approves their own work: writers get a separate reviewer, builders get checks, you approve the gates.
- One fix, then flag; never pipe a chain tool; nothing from memory.
- Stills for checking, contact strips instead of loose frames, one render queue.
- Every run feeds a learning loop: what you pick or correct twice becomes the default.

## Repo layout

```
.claude-plugin/        plugin.json, marketplace.json
skills/explainer-video-workflow/
├── SKILL.md           intake + generation + run instructions
├── references/        interview, writing-style, workflow-steps, script-loop, voice-chain,
│                      footage-and-sourcing, motion-graphics, media-vs-motion, captions,
│                      sourcing-rights, learning-loop
└── templates/         workflow, style, brief, script, b-roll log
```

## Origin

Distilled from a production workflow for a Moroccan-Darija explainer series (voice-first, footage scouted before it is written, graphics on a paper-collage grammar). Everything specific to that series (language, brand, custom render kit) was turned into a question or a placeholder.

## License

MIT
