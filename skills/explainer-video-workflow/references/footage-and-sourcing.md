# Footage scout and b-roll sourcing

Complements `sourcing-rights.md` (rights words, receipts, logs). Order: **scout (search only) → Gate A → download after the voice is final → cut check → log.**

## 1. Footage scout (before any `visual:` line, about 10 min, no downloads)
A cheap search worker takes the 6–12 filmable nouns of the research file or script (a person at the right age, a place, an event, an object, a document) and writes `runs/<id>/scout.md`, one line per noun:
```
AVAILABLE <video-id> <title> <duration> <era seen>
LATER-ERA <video-id> <title> <duration> <era seen>
NONE
```
Search by id and metadata only (the user's search tool, or an API wrapper). The writer then writes `visual:` lines **only from AVAILABLE**; LATER-ERA only when the sentence's time matches the footage's era; NONE becomes a graphic, chart, collage or document. Flag a `visual:` line whose noun is NONE.

Why: in one audit, half of the footage lines named things nobody had filmed honestly.

## 2. Gate A script format (tooling-friendly)
```
## Block 1 · hook
S01 | <sentence>
    visual: <family> <what it shows> | <family> <what it shows>
    src: <url of the fact>
```
One `visual:` entry per shot; families: footage, doc, chart, collage, map, receipt, divider, headline. No "still image" family: a still is a doc, receipt or collage. Every fact has a `src:`.

## 3. Downloading (after the voice is final, and only with the user's yes)
- The **lead** downloads (not a cheap worker). **Probe first** on 3 shots, then the rest: one candidate per `visual:` line. yt-dlp example: `yt-dlp -f "bv*[height<=1080]+ba/b[height<=1080]" -o "brolls/raw/%(id)s.%(ext)s" <id>`. Require at least 720 p; warn on lower, and warn when upscaling beyond about 1.8×.
- **Cookies / bot check:** if the site blocks the download, ask the user to sign in in their browser and pass its cookies (`--cookies-from-browser <browser>`); never bypass a challenge.
- Run long jobs as a script file in the background with a lock per run, never `( … ) &` loops inside the shell.
- Cut ranges with ffmpeg (`-ss`, `-to`, re-encode only the cut), keep the original untouched.
- Receipts (screenshots of a real page with the quoted text located) are captured at readable size: on-screen line height of at least 18 px at the canvas size; crop or use another source otherwise.
- Write `credits.md` at download time: file, source URL, author, licence or the user's rights words.

## 4. Cut check (before the shot list)
For every cut file, take 3 frames at true times and look at **one** contact sheet. A wrong cut (wrong event, wrong era, wrong person) is recut, never kept. Scan cut files for burned-in outlet text or logos (a text detector or a quick look at the sheet): crop, delogo or trim them, or name them.

## 5. Shot list rules
- Footage at most 4 shots in a row; receipts at most 2; graphics at most 2.
- At least one footage shot per 20 s; graphics 20–35 % of runtime.
- The same file at most 4 uses; at least 65 % distinct files; never the same range in two consecutive shots.
- A sentence shorter than about 1.8 s cannot hold its own shot (merge it); footage shots over 5 s get split.
- Each shot has a one-line `why` that names what the file shows.
- English or foreign-language footage with speech gets a translated caption in the user's language.
- Sensitive topics: deaths and accidents get a grey date chip, no slam, no sfx, footage of the place or vehicle, never victims.

## 6. Cleanup
Once scenes are built and checks pass, delete downloaded sources and candidates (`brolls/raw`, `candidates`, previews, logs). Keep what scenes load, the credit files and the voice files. Never delete a file a scene or project file references.
