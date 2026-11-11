# Voice chain (voice first, then everything else)

Runs when the voice exists (`VO=user`, `tts` or `supplied`). The recorded voice is the truth: captions, shot timing and cuts are built from it, never from the script's guessed timing. For `VO=none` skip this file.

## Recording protocol (user records)
1. The script was delivered as numbered chunks `S01…` of 1–2 sentences. The user reads each twice before recording.
2. The user records **each chunk twice**, in one file or one file per chunk, mono 48 kHz WAV if possible (`voiceover-raw.wav`). A short silence between chunks and between takes. A re-start of a sentence is fine; the picker cuts it.
3. The user sends the file(s). From here the run needs no further questions.

## Chain
| # | Step | What to do |
|---|---|---|
| 1 | **Transcribe first** | Run ASR with word timestamps on the raw file (faster-whisper or whisper, `word_timestamps=True`, the user's language). Read the transcript **as a whole**. Compare it with `script.md`. If a sentence reads wrong, repeats, drops its meaning or breaks the flow: fix the script or captions from what was said, or flag the chunk for re-record. Dialect ASR is unreliable: captions keep the script spelling, the voice stays as recorded; list uncertain phrases for the hand-off. |
| 2 | **Pick takes** | For each chunk choose the better take by sound (clean delivery, no stumble, energy), with a forced-align score per take. Read every `MISSING Sxx` and every pick with a low score (below about 0.55). Single take or digits-heavy lines make aligners report false MISSING: align the whole raw file, then cut aborted attempts by time range and re-align. |
| 3 | **Clean** | Denoise always on, then level, then trim dead air (below). Keep `words.json` (per-word start/end) in sync with every cut or speed change. |
| 4 | **Trim dead air** | Gaps over about 0.45 s are audible dead air: shorten to about 0.30 s. Measure the room floor first (raw floors of -49 to -40 dB are common, so a default -45 dB threshold may never fire). |
| 5 | **Audit** | Re-transcribe the cleaned file and diff against the script. **Every** extra word of 0.4 s or more, every stretched or very long word, every too-quiet word, and every phrase said twice in a row is a defect: cut it on the raw by time range and re-align. A defect is never "report only". No clean audit, no build. |
| 6 | **Freeze** | `voiceover-final.wav` and `words.json` are final. Never re-align the final file (timings would drift); re-cut from the raw. Optional speed (`1.1`–`1.2`) rescales `words.json`. |

## ffmpeg recipes (any machine with ffmpeg)
```bash
# denoise + level + mono 48 kHz
ffmpeg -nostdin -i voiceover-raw.wav \
  -af "highpass=f=80,afftdn=nr=12:nf=-40,loudnorm=I=-16:TP=-1.5:LRA=11" \
  -ar 48000 -ac 1 voiceover-clean.wav

# shorten dead air: gaps > 0.45 s become 0.30 s (tune the threshold to the room floor)
ffmpeg -nostdin -i voiceover-clean.wav \
  -af "silenceremove=stop_periods=-1:stop_duration=0.45:stop_threshold=-41dB:stop_silence=0.30" \
  voiceover-final.wav

# loudness map to find the room floor and loud/quiet windows
ffmpeg -nostdin -i voiceover-raw.wav -af "astats=metadata=1:reset=1,ametadata=print:key=lavfi.astats.Overall.RMS_level" -f null -
```
Always pass `-nostdin` to ffmpeg inside shell loops (it eats stdin). Re-run ASR after every trim: trimming changes the timings.

## Supplied audio (`VO=supplied`)
The speaker's words, cleaned, are the captions and the script. Only remove silence and noise; never reword. Pick the concept and example from the source, keep it short, and tell the user which parts were cut.

## AI voice (`VO=tts`)
Skip take picking. Generate per chunk so each chunk has its own file, concatenate with 0.30 s gaps, run align and audit, then freeze.

## After the voice is final
`words.json` exists, so the workers start: b-roll sourcing and motion-graphics scene building together (see `footage-and-sourcing.md`, `motion-graphics.md`). List the remaining steps that do not depend on each other and run them in parallel, at most 3 at a time (leave one core free).
