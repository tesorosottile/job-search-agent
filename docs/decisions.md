# Decisions

Why the system is the way it is. Newest last. Don't re-litigate these, but flag evidence that
one is wrong and ask Gianluigi before changing it.

## Goal

From 1 Feb 2027 he'll work from home in Southern Italy as a consultant for his parents'
companies, possibly with freelance [football mobile game] work, and wants remote part-time work
alongside that; plan B is a full-time role located in Puglia.

## Standing decisions

| Since | Decision |
|---|---|
| 2026-09-27 | A preference is a flag, never an exclusion; he decides on requirements (German, seniority, …) |
| 2026-10-09 | Evidence-bank rule, voice rules and the 350-word cap are the most protected rules |
| 2026-10-09 | Current employer's staff and sister-studio heads on hold until 1 Jan 2027; sister studios never targeted |
| 2026-10-10 | Application language = posting language |
| 2026-10-31 | Gaming, esports and football-media postings may lead with gaming and name the titles |

## Log

| Date | Decision | Why / source |
|---|---|---|
| 2026-11-07 | Scope = remote; Italy or EU-wide; part-time **or** contract/freelance/fractional; business consulting, data analytics, economics | His brief; contract included because consulting part-time work is mostly sold that way (his choice) |
| 2026-11-07 | No scheduled jobs. Three on-demand skills: `/find-jobs`, `/calibrate`, `/draft <ID>` | He runs the loop when he has time |
| 2026-11-07 | Source = LinkedIn in his own logged-in Chrome, read-only, ≤ 50 posting pages per run, stop at any security check | He asked for LinkedIn; its terms prohibit automated access, so the run is kept slow and human-scale |
| 2026-11-07 | Every researched-but-not-picked posting goes to the `seen` list and is never researched again | Otherwise the same 30 rejects would use up the 50-page budget every run |
| 2026-11-07 | Claude fit = predicted **his** score (1–10), not his chance of getting the job; `/calibrate` tracks the mean gap | The gap is what calibration learns from, and the number shows whether it's working |
| 2026-11-07 | `/calibrate` asks one short question per message, no dialogs or tables | He answers by voice |
| 2026-11-07 | `/draft` proposes the narrative and waits before writing anything; outputs live in `applications/<ID>/`, PDFs via Edge | His brief |
| 2026-11-08 | Store = the **Job Quest Board** artifact (an artifact with the db capability): grade high/medium/risky, detail card (requirements, preferences, pay/hours, why), his scores in `scores/*`, gamified (XP, levels, badges). Pay/hours estimates allowed on the card only with a stated basis | His request: readable, works on the phone too |
| 2026-11-09 | LinkedIn moved search to `/jobs/search-results/` (AI search), which ignores the URL filters; `/find-jobs` now writes filters into the query and reads job IDs from `componentkey` | First live run |
| 2026-11-14 | Scope widened with a plan B: **full-time** roles are in scope when **located in Puglia** (on-site, hybrid or remote), same three areas; `/find-jobs` runs a second Puglia search track | His request |
| 2026-11-14 | Public copy (`job-search-agent`) made from the private repo with a fresh history: project and partner names hidden, figures about the employer's projects randomized, personal data and applications left out | He wanted to share the system in an application; the private repo holds personal and employer data |
