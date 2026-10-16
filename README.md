# explainer-video-workflow

A Claude Code skill that runs a repeatable workflow for **short vertical explainer videos** (Reels, Shorts, TikTok, LinkedIn) mixing real b-roll with motion graphics.

It starts by **interviewing you**: your references, your script type and content, your language, your renderer. Then it writes a tailored `WORKFLOW.md` with the steps, gates and rules, and can run the first video with you.

## What you get

```
video-workflow/
├── WORKFLOW.md            ← your tailored steps, gates, read map
├── style-preferences.md   ← brand + references + defaults that learn from each run
└── BRIEF.md               ← fixed brief for scene builders
runs/<run-id>/
├── script.md              ← scene table with retention-loop tags
└── broll.md               ← every asset with source, licence, rights words
```

The workflow, in short:

| # | Step | Stop? |
|---|---|---|
| 0 | Preflight | |
| 1 | Script and shot list using a retention loop (stakes → big question → head fake → rehook) | |
| 2 | Source literal b-roll, log rights | |
| 3 | **Gate A**: script, shots, looks | yes |
| 4 | Build scenes | |
| 5 | QA: zero-token checks, contact sheets | |
| 6 | Assemble and write the post package | |
| 7 | **Gate B**: final cut | yes |
| 8 | Learning: picks become defaults | |

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

In Claude Code, say any of:

- "Make an explainer video workflow for my channel"
- "I want a 60-second Reel from this article"
- `/explainer-video-workflow`

Claude asks 8 short questions in two rounds:

1. **References**: your past videos, other creators (inspiration only), a brand kit, screenshots, or none
2. **Content source**: URL, pasted text, a topic to research, or your footage
3. **Script type**: explainer, news breakdown, story, myth-buster, tutorial, pitch, opinion
4. **Language and voice**: any language or dialect, with or without voiceover
5. **Format**: platform, length, aspect ratio
6. **Renderer**: HTML + headless browser + ffmpeg, Remotion, a manual editor, or plan only
7. **b-roll policy**: own footage, free licences, stock, screenshots for commentary
8. **Gates**: approve plan and cut (normal), or only the cut (auto)

Then it generates the files above and shows you the step table.

## Principles baked in

- Never invent numbers, quotes, receipts or logos. No literal source → the beat becomes an illustration.
- You own the rights decisions. Claude never approves or declares rights for you.
- Nobody approves their own work: builders build, checks and you review.
- Stills for checking, one render queue, contact sheets instead of loose frames, to keep token use low.
- Every run feeds a learning loop: what you pick twice becomes the default.

## Repo layout

```
.claude-plugin/        plugin.json, marketplace.json
skills/explainer-video-workflow/
├── SKILL.md           interview + generation instructions
├── references/        interview, steps, script loop, routing, captions, rights, learning
└── templates/         workflow, style, brief, script, b-roll log
```

## Origin

Distilled from a production workflow for a Moroccan-Darija explainer series. Everything specific to that series (language, brand, custom render kit) was turned into a question or a placeholder.

## License

MIT
