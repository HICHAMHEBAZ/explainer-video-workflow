# Interview question bank

Use `AskUserQuestion`. Two rounds, up to 4 questions per round. Put the recommended option first. "Other" is added automatically. Skip anything already answered.

## Round 1: creative inputs

### Q1 References (header: "References")
Question: "What should this video's look and feel be based on?"
| Option | Meaning | Sets |
|---|---|---|
| My own past videos or brand kit | The user has a style to match | `REF_MODE=own` |
| Other creators' videos | Inspiration only, no reuse | `REF_MODE=inspiration` |
| Screenshots or a mood board | Static references | `REF_MODE=stills` |
| Nothing yet, propose a style | Claude proposes 2 directions at Gate A | `REF_MODE=none` |
Follow-up in plain chat: "Paste the links or file paths, and in one line say what to copy (frame, captions, pacing, colours, b-roll style) and what not to copy."
Output: fill `{{REFERENCES}}` and `{{COPY_NOT_COPY}}` in `style-preferences.md`. A reference is described in words (grid, caption position, pacing, palette). Never store another creator's footage or logo in the project.

### Q2 Content source (header: "Source")
| Option | Sets |
|---|---|
| An article or URL | `SOURCE=url` (read it at the script step) |
| Pasted text or notes | `SOURCE=text` |
| A topic, research it for me | `SOURCE=research` (needs web tools; cite every claim) |
| My own footage and a rough idea | `SOURCE=footage` (b-roll step becomes a footage review) |

### Q3 Script type (header: "Script type")
| Option | Loop emphasis |
|---|---|
| Explainer (how or why something works) | Head fakes from the mechanism; MOTION-heavy middle |
| News breakdown | Stakes from "what changes for you"; receipts (headlines, filings) as MEDIA |
| Story or case study | One character; chronology; MEDIA-heavy with archive footage |
| Myth-buster | Head fake is the structure: expected belief, then the reversal |
Additional types (user can pick "Other"): tutorial, product or pitch, opinion. For these, set `LOOP=light` (stakes, one question, one reveal, a closing question) and warn that the retention loop is built for informational content.
Output: `{{SCRIPT_TYPE}}`, `{{LOOP_EMPHASIS}}`.

### Q4 Language and voice (header: "Language")
Ask the language or dialect in the question text (default: the language the user is writing in). Options for voice:
| Option | Sets |
|---|---|
| Captions only, no voiceover | `VO=none`, captions timed at ~2.4 words per second |
| I will record a voiceover | `VO=user`, re-time captions to audio after the recording |
| AI voiceover | `VO=tts`, ask which tool; re-time to the audio |
| Not sure yet | `VO=none`, revisit at Gate B |
Also ask (plain chat) for: dialect spelling conventions, words to avoid, and a tone phrase ("a friend at a café", "newsroom", "teacher"). Output: `{{LANGUAGE}}`, `{{VOICE_RULES}}`, `{{RTL}}` (true for Arabic, Hebrew, Persian, Urdu).

## Round 2: production inputs

### Q5 Format (header: "Format")
| Option | Sets |
|---|---|
| 9:16, 60 s (Recommended) | 1080×1920, 30 fps, 15 beats, 120–140 spoken words |
| 9:16, 30 s | 8 beats, 60–70 words |
| 9:16, 90–150 s | scale beats, add a brand sting after the hook |
| 16:9 or 1:1 | change safe zones; warn that the layout rules in this skill assume 9:16 |
Ask the platforms (Reels, Shorts, TikTok, LinkedIn) in chat; they decide the post-package files.

### Q6 Renderer (header: "Renderer")
| Option | Effect on the workflow |
|---|---|
| HTML scenes + headless browser + ffmpeg | Full pipeline: scene pages, stills for checking, one render queue, assemble script |
| Remotion | Scenes are React compositions; stills via `remotion still`; render queue via `remotion render` |
| Manual editor (CapCut, Premiere, DaVinci, After Effects) | Build step produces a scene spec per beat (shot, motion, caption chunks, timing) for the editor; no render queue or lint |
| Plan only | Stop after Gate A; deliver script, shot list, sourcing log, motion briefs |
Output: `{{RENDERER}}`, and which of steps 4, 5, 6 apply (see `workflow-steps.md`).

### Q7 b-roll policy (header: "b-roll")
| Option | Rights rule |
|---|---|
| Own footage only | No sourcing; user supplies files |
| Free licences (Wikimedia Commons, NASA, public-domain archives) | Log licence and author per asset; credit in the post |
| Stock sites as well | Allowed only because the user chose it; log the licence |
| Screenshots of public sources for commentary | Real page, real quote, source shown; never redrawn |
Multi-select allowed. Output: `{{BROLL_POLICY}}`. Social and web video is never fetched unless the user states a rights declaration in chat.

### Q8 Gates (header: "Gates")
| Option | Sets |
|---|---|
| Normal: approve the plan, then the final cut (Recommended) | `MODE=normal` |
| Auto: stop only at the final cut | `MODE=auto` |
Also ask where approval happens: chat only, or a shared board (an artifact or doc). Default chat: number the beats, the user answers "approve" or a note per number.

## After the interview
Echo the answers back as a 6-line summary before writing files. If the user corrects anything, update the variables, then generate.
