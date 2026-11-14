# job-search-agent

My job search, run as a small agent system on Claude Code. I'm Gianluigi Sottile, an economist
(MSc LMU Munich) looking for remote part-time work in business consulting, data analytics and
economics from February 2027, with a full-time role in Puglia as plan B.

This is the public copy of a private repository. Same skills, same rules, same files; the
private bits are hidden or changed (see [What's changed in this copy](#whats-changed-in-this-copy)).

Nothing runs on a schedule: it's a loop I run when I have time, with a clear line between what
the agent does and what stays mine.

## The loop

| Step | Who | What happens |
|---|---|---|
| **`/find-jobs`** | Agent | Reads up to 50 new LinkedIn postings in my logged-in browser, read-only and slowly, and gives each a **fit score** (1–10): its prediction of how I'd rate the posting, based on my preferences ([`profile/scoring-principles.md`](profile/scoring-principles.md)) and my skills and experience ([`profile/evidence-bank.md`](profile/evidence-bank.md)). The top ≤ 20 go on a board with a grade, the requirements matched against my evidence, and the reasons. The rest go to a `seen` list and are never researched again. |
| **Rate** | Me | I give each posting on the board my actual score, 1–10, with an optional note and a status. |
| **`/calibrate`** | Agent + me | Optional. Asks me a few short questions about why I scored postings the way I did (I answer by voice) and turns my answers into rules in [`profile/scoring-principles.md`](profile/scoring-principles.md), which the next search uses. The gap between predicted and actual scores is logged, so I can see whether it's learning. |
| **`/draft <ID>`** | Agent + me | Proposes how to pitch me for that job and **stops**. Only after I agree does it write what I asked for: CV, letter, form answers. |
| **Apply** | Me | I edit and send. The agent never submits, uploads or messages anyone. |

The skills live in [`.claude/skills/`](.claude/skills/). The operating manual and hard rules are
in [`CLAUDE.md`](CLAUDE.md); the reasoning behind each choice is in
[`docs/decisions.md`](docs/decisions.md).

## Where the agent stays out

Two places:

1. **Facts about me.** Every claim in a CV, letter or form answer must trace to an entry in
   [`profile/evidence-bank.md`](profile/evidence-bank.md). Every edit to it is mine, or made at
   my request in my own words. The agent can't infer, round up or "reasonably extrapolate".
2. **Decisions.** Which jobs I rate highly, which I apply for, and what gets sent are mine. The
   skills can't write my ratings, and nothing applies, submits or messages anyone on my behalf.

Everything the agent writes also follows [`profile/voice.md`](profile/voice.md): no stock
cover-letter phrases, letters capped at 350 words.

## The board

[`board/board.html`](board/board.html) is the source of the Job Quest Board, a Claude artifact
with a small database: one row per posting, a detail card (requirements, preferences, pay and
hours with their source, reasons with evidence IDs), and my scores. It's gamified because I'm
more likely to open it that way. The live board and its data are private.

## LinkedIn

`/find-jobs` reads LinkedIn through my own account in my own browser. LinkedIn's terms don't
allow automated access, so the skill is deliberately human-scale: one tab, a few seconds between
pages, at most 50 posting pages per run, read-only (no applying, saving, following or
messaging), and it stops at the first CAPTCHA or security check instead of getting past it.

## What's changed in this copy

The private repository holds personal data and figures that belong to my employer's projects.
In this copy:

- **Project and partner names are hidden**, shown as `[game title]`, `[football mobile game]`,
  `[a major game publisher]` and similar.
- **Figures about my employer's projects are randomized**: product sales, store visits,
  wishlists, purchases, social-media reach, ad counts. The structure and the methods are real;
  those numbers are not. My own academic figures (dataset size, grades) are unchanged.
- **Personal data is removed**: phone, email, referee, local paths. CV and letter templates use
  `{{EMAIL}}` and `{{PHONE}}`.
- **Left out entirely**: my applications (posting texts, drafts, notes), my library of
  application narratives, one family-related evidence entry, the live board and its scores, and
  the private repository's history.
- **Discretion rules** about my current employer are kept, without naming its sister studios.

## Running it yourself

You'd need Claude Code, the Claude in Chrome extension for `/find-jobs`, and your own
`profile/` (evidence bank, CV master, voice). Publish `board/board.html` as an artifact with the
`db` capability and put its URL where the skills say `<your board artifact URL>`.
