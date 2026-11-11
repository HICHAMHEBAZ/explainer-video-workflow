# Intake question bank

Use `AskUserQuestion`. Round 1 is always the three creative questions (references, writing style, aspect ratio) before anything else; round 2 is production. At most 4 questions per round. Put the recommended option first ("Other" is added automatically). Skip anything already answered.

## Round 1: creative inputs (always first)

### Q1 References (header: "References")
Question: "What should this video's look, sound and feel be based on?"
| Option | Meaning | Sets |
|---|---|---|
| My own past videos or brand kit | The user has a style to match | `REF_MODE=own` |
| Other creators' videos | Inspiration only, no reuse | `REF_MODE=inspiration` |
| Screenshots or a mood board | Static references | `REF_MODE=stills` |
| Nothing yet, propose a style | Two directions proposed at Gate A | `REF_MODE=none` |

Follow-up in plain chat: "Paste the links or paths, and in one line say what to copy (frame, captions, pacing, colours, b-roll style, sound) and what not to copy."
Output: `{{REFERENCES}}`, `{{COPY}}`, `{{DO_NOT_COPY}}`. A reference is described in words (grid, caption position, pacing, palette, cut rhythm). Never store another creator's footage or logo in the project.

### Q2 How you write (header: "Writing")
Question: "How should the script sound?"
| Option | Sets |
|---|---|
| I will paste sample scripts or captions, match them | `WRITE_MODE=sample`: extract the style from the samples (see `writing-style.md`) |
| I will describe it | `WRITE_MODE=described`: ask the follow-ups below |
| Match my references | `WRITE_MODE=refs`: derive from the reference videos' narration |
| No style yet, propose one | `WRITE_MODE=propose`: write two short sample hooks at Gate A, user picks |

Plain-chat follow-ups (only the unanswered ones):
1. The one viewer, in a sentence.
2. Language, dialect or register, and spelling conventions.
3. Sentence length and rhythm (short and punchy, or flowing).
4. Person and tone (I / you / we; "a friend at a café", "newsroom", "teacher").
5. Report-only, or opinion allowed.
6. Words, phrases and openings to never use.

Output: the `## Writing` section of `style-preferences.md`: `{{VIEWER}}`, `{{LANGUAGE}}`, `{{REGISTER}}`, `{{RHYTHM}}`, `{{TONE}}`, `{{STANCE}}`, `{{AVOID_WORDS}}`, `{{RTL}}` (true for Arabic, Hebrew, Persian, Urdu).

### Q3 Aspect ratio and format (header: "Format")
| Option | Sets |
|---|---|
| 9:16 vertical (Recommended) | 1080×1920; Reels, Shorts, TikTok |
| 4:5 portrait | 1080×1350; Instagram feed |
| 1:1 square | 1080×1080; feeds, LinkedIn |
| 16:9 landscape | 1920×1080; YouTube, LinkedIn, web |

Ask in chat: length (default 60 s; 30 s shorter; 90–180 s needs a bigger idea) and platforms.
Output: `{{ASPECT}}`, `{{CANVAS}}`, `{{LENGTH}}`, `{{FPS}}` (default 30; 24 for a filmic look), `{{PLATFORMS}}`, `{{BEATS}}`, `{{WORDS}}` (about 2.4 spoken words per second), and the safe-zone row from `captions.md`. Export at the canvas size; a smaller export (720 p) is fine if the user wants it faster.

## Round 2: production inputs

### Q4 Content source and script type (header: "Source")
Source: an article or URL (`SOURCE=url`); pasted text or notes (`text`: keep its angle, research only what it leaves thin); a topic to research (`research`: cite every claim, keep a research file); own footage and a rough idea (`footage`).
Script type: explainer, news breakdown, story or case study, myth-buster, tutorial, product or pitch, opinion. Sets `{{SCRIPT_TYPE}}`. For tutorial, pitch and opinion use `LOOP=light`.

### Q5 Voice (header: "Voice")
| Option | Sets |
|---|---|
| I record it myself | `VO=user`: chunks recorded twice, voice chain runs (`voice-chain.md`) |
| AI voiceover | `VO=tts`: ask which tool; skip take picking, keep alignment and audit |
| Supplied audio (a speaker's own words) | `VO=supplied`: silence removal only; captions follow the words |
| Captions only | `VO=none`: captions at about 2.4 words per second; voice steps skipped |

Output: `{{VO}}`, `{{VOICE_RULES}}`.

### Q6 Renderer (header: "Renderer")
| Option | Effect |
|---|---|
| HTML scenes + headless browser + ffmpeg | Full pipeline: scene pages, stills, lint, one render queue, assemble |
| Remotion | Scenes are React compositions; stills via `remotion still`; `remotion render` |
| Manual editor (CapCut, Premiere, DaVinci, After Effects) | Build step produces a scene spec per beat for the editor; no lint or render queue |
| Plan only | Stop after Gate A: script, shot list, scout file, motion briefs |

### Q7 b-roll policy and rights (header: "b-roll")
Multi-select: own footage only · free licences (Wikimedia Commons, NASA, public domain) · stock sites · **YouTube or social clips** (allowed only when the user states a rights declaration in chat; record it verbatim; the footage must show the story it captions) · screenshots of public sources for commentary (real page, real quote, never redrawn).
Output: `{{BROLL_POLICY}}`.

### Q8 Gates (header: "Gates")
Normal (stop at the script, then the final cut; recommended) or auto (stop only at the cut). Also ask where approval happens: chat only (default; number the chunks, the user answers "approve" or a note per number) or a shared board.

## After the intake
Echo the answers back as a six-line summary before writing files. If the user corrects anything, update the variables, then generate.
