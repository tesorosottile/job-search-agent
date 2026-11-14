---
name: calibrate
description: Learn Gianluigi Sottile's job preferences from the scores he gave on his Job Quest Board. Compares his 1-10 scores with Claude's predicted fit, asks him a few short spoken-style questions (he answers by voice), and turns his answers into general principles in profile/scoring-principles.md, which /find-jobs uses next time. Use when he says /calibrate, "learn from my scores" or "I scored some jobs".
---

# /calibrate

He has rated postings on his **Job Quest Board**
(`<your board artifact URL>`): a 1–10 score, sometimes a note. You find
out *why*, in a short conversation, and write the general principles into
`profile/scoring-principles.md`, so the next `/find-jobs` predicts him better.

## 0. Setup

1. Read `profile/scoring-principles.md`.
2. Load `ArtifactData`; `list` the `postings` and `scores` collections (page with
   `query.cursor` until done). His rating for posting `<num>` is `scores/<num>`
   (`score`, `notes`, `status`).
3. **New scores** = postings with a `scores/<num>.score`, no `calibrated` field, and no
   `example: true`. If there are none, say "No new scores yet. Rate some quests on the board
   first." and stop. For context, read `applications/<num>/posting.md` for the ones you'll ask
   about.

## 1. Find what to ask (silently)

For each new score, gap = `score − fit` (fit = Claude's prediction on the posting). Look for:
- the biggest misses in both directions (|gap| ≥ 2);
- patterns across rows (type, hours, pay, area, company kind, language, remote scope) that the
  current principles don't explain;
- notes that hint at a reason without stating it.

Plan **at most 5 questions**, most informative first. Don't ask about rows where the current
principles already predicted him within 1 point, unless his note contradicts the principle.

## 2. Ask: voice first

He answers **by voice** (dictated, so you get a transcript). Write every message so it works
read aloud and answered out loud:

- **One question per message**, one or two short sentences. No tables, bullets, headings or
  links. Don't use multiple-choice dialogs (AskUserQuestion): he'd have to tap.
- Name the job by company and plain title ("the part-time pricing role at Acme"), never by ID only.
- Ask about the reason, not the number: "You gave it a nine, I'd guessed five. What made it a nine?"
- Read the transcript generously. Dictation garbles names and numbers; if the meaning is
  unclear, read your understanding back in one sentence instead of guessing.
- Open the next message with what you understood, then the next question:
  "Got it: you'd rather have fixed hours than freelance on demand. Next: …"
- "Skip" moves to the next question; "stop" or "enough" goes to step 3.

## 3. Confirm, then write

Read back the principles you'll save, as one short spoken-style list ("I'll save three things:
one, … two, … three, …. OK?"). Change them as he says. Then edit `profile/scoring-principles.md`:

- **Learned from his scores**: one **general** principle per line (a rule that would rank a
  future posting, not "posting 14 was good"), then `(YYYY-MM-DD; postings N, N)`. Remove the
  "_None yet._" placeholder.
- Merge near-duplicates. If a new principle contradicts an older one, keep his latest view,
  delete the old line, and tell him you did.
- Delete any **starting guess** a learned principle now covers.
- **Scope** and **Hard excludes** change only if he explicitly says so ("include full-time too").
  Say back what changed.
- Add a **Calibration log** row: date · the posting numbers · mean |fit − score| over them
  (one decimal). Over time this number should fall; if it doesn't, say so.
- Keep the file readable in two minutes: tighten wording rather than adding lines.

Then mark the postings learned: one `ArtifactData` `batch` of `update` on each
`postings/<num>` with `{"calibrated": "<YYYY-MM-DD>"}`, pinned to the `version` you read
(every new-score posting, asked about or not). If a pin is refused, re-read that doc and redo it.

## 4. Commit and close

Commit with GitHub Desktop's git:
`$g = (Get-ChildItem "$env:LOCALAPPDATA\GitHubDesktop\app-*\resources\app\git\cmd\git.exe" | Sort-Object FullName | Select-Object -Last 1).FullName`,
`& $g add profile/scoring-principles.md`,
`& $g commit -m "calibrate: <n> principles from postings <nums>"` (with the Co-Authored-By trailer). Don't push.

End with one spoken-style line: how many principles were added or changed, and the new mean gap.

## Never

- Write the `scores` collection (his ratings, notes and status), or any posting field other
  than `calibrated`.
- Put facts about him in the evidence bank. If he mentions something new about himself
  ("I did pricing for my dad's shop"), ask once: "Want me to add that to your evidence bank,
  in those words?" Add it only on a clear yes, quoting him, with today's date as the source.
- Turn one posting's quirk into a principle. If you can't state it generally, leave it out.
