# Writing: the user's voice, built on the content principles

Two layers, in this order:
1. **Method = the content principles** (how a viewer's mind works). They decide how every script, hook, caption set and post is *built*.
2. **Voice = the user's style** (captured at intake). It decides how the words *sound*, plus the hard constraints (stance, language rules, safe wording).

**Precedence:** the principles are first, mainly and always. The style file and the format only add hard constraints (language, stance, caption chunk caps); they never choose the structure. A format file that prescribes a shape (hook formula, scene count, word budget) is overridden by the principles.

If the skill `content-principles` ([aiwithremy/content-principles](https://github.com/aiwithremy/content-principles)) is installed, **load it before writing** and treat it as the full method; this file is the portable summary for when it is not. Not copied here: it is the author's text.

## The stance: think, don't pattern-match
- No spine, no template, no counts to hit, no hook formula. Reason from the viewer's psychology for this one idea; the structure falls out and differs every run.
- **Apply silently.** Never print the principles, a checklist, a score or "hook type: X" in the chat or in files.
- **Formula-mode alarms:** you chose a structure before understanding the idea; the script survives swapping the subject; you can name the format; you adapted an old hook. Any one = throw it out and start from the viewer.
- They are priors, not rules: a compelling script that breaks them beats one that ticks them.

## The principles
1. **One person, and you are sending it to them.** Write to one real viewer who just met this idea in their feed, not "the audience". No greeting, no performed enthusiasm, no explaining what they know. Specificity goes in the object (number, name, date), never in a named viewer job.
2. **The two scroller questions: value, and time cost.** They are a ratio; the opening makes value feel big and cost feel small. 60 s is already long; a longer video needs a bigger gap. **The gap between what you know and what they know is the product.** No gap, no video.
3. **Read line by line, not as a whole.** Does line 1 sell line 2, and line 2 line 3? Each line gives exactly enough to make the next necessary (progressive disclosure), never more.
4. **Curiosity loops.** A loop is a question the viewer is holding. The hook is the first loop, not a trick. Open the question before answering it; never close the last loop before the next opens; open a fresh one about 60–70 % in, after the promise is paid. The viewer must be the one holding the question (an on-screen interviewer being curious is not a loop). Never deflate a loop you opened.
5. **Specificity.** In every sentence ask whether a number, name or date can replace a broad summary ("45 days ago", not "a while back"). Open on a specific object, not a category.
6. **Unique ideas, simply explained.** The 10-year-old test on every line: simplify the sentence, never the idea; keep a technical term only if it is the precise word and explain it in the same line. A good idea fits in ten words; if it needs thirty it is muddy. A story needs a shocking concrete fact inside 10 s.
7. **Value per second.** Value promised in the first 3 s; the first genuinely useful or surprising fact *delivered* by 5–10 s. Move forward as fast as the idea allows; the premise is not the content. (Platforms test on a small sample first; the opening is what the distribution system measures.)
8. **Cut the fluff.** One centre of gravity (the thing learned, witnessed, tested or awaited). A line that is interesting but not relevant goes, even a favourite. No preamble, no "why I'm making this", no dead second. Words are cheap, ideas are dear: short sentences (mean under about 9 words) beat long ones (16+). Count words honestly in the user's language.
9. **Preempt the live objection** ("this is an ad", "I've seen this", "this won't work for me", "this takes forever"): know which one this video provokes and disarm it in a short aside right where the doubt lands.
10. **The frame.** Visual rhythm is how long any one frame is held. Write distinct beats so the edit has places to cut; the same footage in several short visits beats one long visit; loops create attention, cuts only refresh it. A pure talking head with no cutaways is usually the weakest option.

## Capturing the user's voice (intake Q2)
- **Samples** (best): ask for 2–3 past scripts, captions or transcripts; describe the style in words in `style-preferences.md` → `## Writing`: viewer, register and dialect, mean sentence length, how a typical hook opens, how numbers are said, person (I / you / we), humour, what the voice never does. Quote at most one short line.
- **Described:** turn the answers (viewer, language, rhythm, tone, stance, avoid-list) into the same section. Ask the viewer question if unanswered: what they do, what they already know, what hurts, what they want.
- **References:** describe the narration of the reference videos; never copy sentences.
- **Propose:** write two 15-second sample hooks in different styles, let the user pick, record it.
- Language rules the user states (dialect forms, spelling, words to avoid, terms kept in the standard language) go in verbatim. Keep a table of preferred forms and update it whenever the user corrects a word. Never call dialect copy "verified"; a native speaker should read it once. Technical terms with no clean word in the dialect stay in the standard language; do not invent words.

## Stance constraints (hard, set at intake)
- **Report-only:** what was said, by whom, where, and what the record shows. Attribution inside the sentence; computed numbers labelled as computed; no verdict, no closing take; a hook may open a loop but may not decide it, and is never built on outrage or a claim the record does not support.
- **Opinion allowed:** mark opinion as opinion; facts still need a source.
- **Narrow angle:** one case or question, few figures; cut what does not serve it.
- Never name a source on screen or in narration if the user chose that; sourcing then lives in `credits.md` and the research file.

## Process (every run, any format)
1. Load the principles (and the style file). Read the user's preferences and lessons.
2. Name the one viewer and the one gap in one line **for yourself** (not in the deliverable).
3. Write the draft **without a structure in mind**; then read it as that viewer, line by line, cutting what does not sell the next line.
4. **A separate reviewer** (different subagent or session, not the writer) checks facts against the research file, the user's language rules, the stance, and gives an honest principles read (does line 1 sell line 2, any fluff, any formula-mode sign). It fixes in place before the user sees the script.
5. Deliver in the chat, full text, as **numbered chunks of one or two sentences** (`S01`, `S02` …) so the user can record chunk by chunk, plus a five-line note (angle, where loops open, weak sources, uncertain phrases, length estimate). Working copy `runs/<id>/script.md`.

## Supplied text
Keep its idea and facts (thesis in one line, what it leaves thin). Research only the gaps and cite them. Then rewrite from the viewer's side with the principles, not by re-pouring it into a shape. After the script, one chat line: the idea kept, what was added, where the loops open.

## Captions and posts
Same method. Caption chunks must also meet the build caps in `captions.md`. Post copy: each line sells the next, a specific object over a category, no fluff.
