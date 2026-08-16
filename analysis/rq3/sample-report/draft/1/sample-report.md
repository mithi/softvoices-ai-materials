# RQ3 — Patterns *(illustrative fake data)*

**Question.** What patterns emerge across sessions, agent roles, response length, reaction and flagging behavior, and interview themes?

**Data.**
- N = 24. Six sessions. Eight roles in a **fixed order**.
- Not every role fires every session. Comments appear two at a time (`Load more`), but the revisited response is locked until **every** generated comment has been shown.
- Reactions are one of 🔔 raised something new, 🤔 worth sitting with, 🔄 shifted my view, 🤷 didn't land — or none.
- 🚩 is a separate action (can sit on top of a reaction).

**Descriptive only.**
- Role differences may be the role, the **order**, or **how often the role fired**. Do not read any figure as “this role works better.”
- Person is the unit where a rate is averaged (session trends, usefulness, habits, trust, tagging intensity). Comment counts are totals across people.

---

## 0. Exposure (read this before any role chart)

Later roles **fire** less often (not every role applies to every post). They are not hidden: every generated comment is shown before revisit. `n` below is comments that existed — all of them were on screen. “Didn’t notice” at end-of-study is recall, not a skipped `Load more`.

| role (session order) | n comments | any reaction | flagged | didn’t notice (of 24) |
| --- | --- | --- | --- | --- |
| Charitable Reader | 144 | 86 | 2 | 0 |
| Steelmanner | 144 | 96 | 3 | 1 |
| Perspective Shifter | 120 | 70 | 1 | 2 |
| Historian | 72 | 36 | 4 | 8 |
| Warrant Surfacer | 100 | 58 | 2 | 3 |
| Empiricist | 80 | 38 | 6 | 6 |
| Frame Skeptic | 90 | 46 | 3 | 4 |
| Conceptual Clarifier | 70 | 34 | 1 | 9 |
| **Total** | **820** | **464** | **22** | — |

**Read.**
- Charitable Reader and Steelmanner always applied (144 = 24 × 6). Historian and Conceptual Clarifier applied less often.
- 9 people still said they didn’t notice Conceptual Clarifier at the end — they saw those comments; the voice didn’t stick, or it rarely fired for them.
- Any “later roles got fewer 🔄” claim has to survive this table (applicability, not dropout).

---

## 1. Role-level usefulness and “didn’t notice”

End-of-study, one rating per role. Means use only people who gave 1–7. “Didn’t notice” is not a 1.

- **A.** Each **dot** is one person who remembered the role. **Diamond** = mean ± 1 SD. Dashed line = midpoint (4).
- **B.** Count who chose “Didn’t notice.”

![Role-level usefulness and didn’t notice](./img/01_usefulness_and_notice.png)

| role | n rated | n didn’t notice | mean | SD |
| --- | --- | --- | --- | --- |
| Charitable Reader | 24 | 0 | 5.2 | 1.0 |
| Steelmanner | 23 | 1 | 5.6 | 1.0 |
| Perspective Shifter | 22 | 2 | 5.0 | 0.9 |
| Historian | 16 | 8 | 4.3 | 0.9 |
| Warrant Surfacer | 21 | 3 | 5.4 | 0.8 |
| Empiricist | 18 | 6 | 4.8 | 1.4 |
| Frame Skeptic | 20 | 4 | 3.9 | 1.2 |
| Conceptual Clarifier | 15 | 9 | 4.5 | 1.1 |

**Read.**
- Steelmanner and Warrant Surfacer sit highest among people who remember them.
- Frame Skeptic is the only mean below 4.
- Historian and Conceptual Clarifier are missing for a third of the sample — don’t compare their means to Charitable Reader’s as if they had the same n.

**Most / least named** (open text; recall, not a test):

| named as helped most | n | named as helped least / annoyed | n |
| --- | --- | --- | --- |
| Steelmanner | 8 | Frame Skeptic | 7 |
| Warrant Surfacer | 6 | Historian | 5 |
| Charitable Reader | 4 | Conceptual Clarifier | 4 |
| Perspective Shifter | 3 | Steelmanner | 3 |
| Empiricist | 2 | Empiricist | 2 |
| other / none | 1 | other / none | 3 |

Steelmanner appearing on **both** lists is the finding: polarizing, not “best.”

**Person-level usefulness** (— = didn’t notice):

| participant_id | Charitable | Steelmanner | Perspect. | Historian | Warrant | Empiricist | Frame Sk. | Concept. |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 6 | 6 | 5 | 6 | 6 | 4 | 2 | 5 |
| 2 | 5 | 4 | 6 | 5 | 5 | 5 | 6 | 4 |
| 3 | 5 | 5 | 5 | 4 | 6 | 6 | 6 | 4 |
| 4 | 5 | 5 | 6 | 4 | 5 | 4 | 4 | 4 |
| 5 | 5 | 5 | 5 | 4 | 6 | 5 | 4 | 5 |
| 6 | 4 | 7 | 6 | 6 | 4 | 4 | 4 | 6 |
| 7 | 5 | 5 | 6 | 4 | 6 | 7 | 3 | 5 |
| 8 | 6 | 6 | 4 | 4 | 4 | 5 | 5 | 4 |
| 9 | 5 | 7 | 5 | 5 | 4 | 5 | 3 | 5 |
| 10 | 5 | 5 | 5 | 4 | 5 | 4 | 4 | 7 |
| 11 | 7 | 5 | 5 | 3 | 5 | 6 | 3 | 3 |
| 12 | 7 | 6 | 4 | 3 | 6 | 3 | 3 | 4 |
| 13 | 6 | 6 | 4 | 4 | 7 | 4 | 2 | 4 |
| 14 | 4 | 4 | 5 | 4 | 5 | 5 | 6 | 3 |
| 15 | 5 | 6 | 6 | 5 | 5 | 2 | 4 | 5 |
| 16 | 6 | 7 | 6 | 4 | 6 | 7 | 5 | — |
| 17 | 4 | 4 | 4 | — | 6 | 3 | 4 | — |
| 18 | 5 | 7 | 4 | — | 5 | 7 | 3 | — |
| 19 | 3 | 6 | 6 | — | 5 | — | 3 | — |
| 20 | 6 | 5 | 3 | — | 6 | — | 3 | — |
| 21 | 4 | 7 | 5 | — | 6 | — | — | — |
| 22 | 5 | 6 | 5 | — | — | — | — | — |
| 23 | 5 | 4 | — | — | — | — | — | — |
| 24 | 6 | — | — | — | — | — | — | — |

---

## 2. Reactions by role — counts, not 100% stacks

Clustered bars. Y = **count of comments**. Four bars per role. Untagged is left out of the bars (it would swallow the chart) and kept in the table. Roles are not sorted by “best.”

![Reactions by role, clustered counts](./img/02_reactions_counts_by_role.png)

| role | n | 🔔 | 🤔 | 🔄 | 🤷 | untagged | % tagged | % 🔄 | % 🤷 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Charitable Reader | 144 | 32 | 28 | 8 | 18 | 58 | 60 | 6 | 12 |
| Steelmanner | 144 | 20 | 24 | 22 | 30 | 48 | 67 | 15 | 21 |
| Perspective Shifter | 120 | 22 | 18 | 14 | 16 | 50 | 58 | 12 | 13 |
| Historian | 72 | 10 | 12 | 6 | 8 | 36 | 50 | 8 | 11 |
| Warrant Surfacer | 100 | 14 | 22 | 12 | 10 | 42 | 58 | 12 | 10 |
| Empiricist | 80 | 8 | 14 | 10 | 6 | 42 | 48 | 12 | 8 |
| Frame Skeptic | 90 | 12 | 10 | 4 | 20 | 44 | 51 | 4 | 22 |
| Conceptual Clarifier | 70 | 8 | 12 | 5 | 9 | 36 | 49 | 7 | 13 |

**Read the counts (the figure).**
- Most tagging sits on the first two roles — they applied every session.
- Steelmanner has the most 🔄 (22) **and** the most 🤷 (30).
- Frame Skeptic’s 🤷 bar (20) is high even though that role fired less often than the openers.
- Charitable Reader’s 🔄 bar is short (8).

**Read the percents (the table, not the figure).**
- 🔄 is 6% of Charitable Reader comments vs 15% of Steelmanner and 12% of Empiricist.
- Empiricist’s 🔄 *count* (10) is unremarkable; its *rate* is not.
- Frame Skeptic’s 🤷 *rate* (22%) matches Steelmanner’s (21%) — the count chart alone would make Steelmanner look like the only one that didn’t land, because it had more chances.

That is why the figure is counts and the table is both. A 100% stacked bar would have made Empiricist and Historian look as “big” as Charitable Reader.

---

## 3. Are a few people doing all the tagging?

Each dot = that person’s % of *their* comments that got any reaction. Diamond = mean ± 1 SD.

![Tagging intensity](./img/03_tagging_intensity.png)

| measure | mean | SD | min | max | n |
| --- | ---: | ---: | ---: | ---: | ---: |
| % of comments tagged | 37 | 15 | 6 | 71 | 24 |

**Read.** Two people sit near the top; a few sit under 10%. Figure 2 is not “the group.” It is a mix of heavy and quiet taggers.

---

## 4. Reactions across sessions

Y = each person’s **% of comments that session** with that reaction, then the mean of 24. Band = ±1 SD. Y runs 0–40 so a 4-point wiggle is not a cliff. Black line = fit through the 6 means (a ruler for tilt, not a claim that the path was straight).

![Reaction rates across sessions](./img/04_reaction_rates_by_session.png)

| % of comments (mean of 24 people) | S1 | S2 | S3 | S4 | S5 | S6 |
| --- | --- | --- | --- | --- | --- | --- |
| raised new | 16.0 | 15.0 | 14.0 | 13.5 | 14.2 | 12.6 |
| sit with | 18.1 | 17.1 | 16.1 | 15.2 | 14.4 | 14.6 |
| shifted view | 14.1 | 12.4 | 11.7 | 9.2 | 10.2 | 8.1 |
| didn't land | 14.1 | 15.3 | 13.6 | 16.2 | 14.0 | 15.0 |

Raw 🔄 **counts** (same comments, no person-averaging): S1 18, S2 16, S3 14, S4 11, S5 12, S6 10. Same tilt. Counts here are safer than in Figure 2 because each session has a similar number of comments (~136–140). Still report the %.

**Read.**
- 🔄 eases off after session 1. 🤷 does not.
- That is closer to “the shift reaction got rarer” than to “people got more annoyed.”
- Session ≠ post; if one session dips, check the same rates by post before inventing a boredom story.

---

## 5. Response length

**Figure 5a.** Each person: mean word count across 6 initials vs 6 revisited. Grey line = the pair. Diamond = group mean ± 1 SD.

![Paired response length](./img/05a_length_paired.png)

**Figure 5b.** Session means, two lines, ±1 SD band. No person dots on the lines.

![Response length across sessions](./img/05b_length_by_session.png)

| mean words (SD) | S1 | S2 | S3 | S4 | S5 | S6 |
| --- | --- | --- | --- | --- | --- | --- |
| initial | 87 (20) | 89 (23) | 88 (17) | 78 (19) | 76 (14) | 75 (20) |
| revisited | 123 (25) | 116 (28) | 117 (21) | 108 (20) | 104 (25) | 100 (26) |

Person-level means (plotted in 5a) plus tagging rate (Figure 3):

| participant_id | initial words | revisited words | % tagged |
| --- | --- | --- | --- |
| 1 | 68 | 111 | 24 |
| 2 | 72 | 94 | 46 |
| 3 | 66 | 90 | 28 |
| 4 | 89 | 122 | 35 |
| 5 | 74 | 67 | 18 |
| 6 | 49 | 77 | 16 |
| 7 | 105 | 128 | 71 |
| 8 | 80 | 103 | 29 |
| 9 | 94 | 126 | 43 |
| 10 | 89 | 104 | 37 |
| 11 | 104 | 124 | 30 |
| 12 | 91 | 86 | 29 |
| 13 | 102 | 145 | 49 |
| 14 | 89 | 120 | 33 |
| 15 | 95 | 124 | 35 |
| 16 | 90 | 125 | 38 |
| 17 | 66 | 100 | 59 |
| 18 | 75 | 123 | 50 |
| 19 | 78 | 116 | 45 |
| 20 | 82 | 133 | 28 |
| 21 | 67 | 97 | 6 |
| 22 | 100 | 140 | 55 |
| 23 | 83 | 122 | 55 |
| 24 | 69 | 94 | 35 |

| | initial | revisited |
| --- | ---: | ---: |
| person-mean | 82 | 111 |
| SD | 14 | 20 |

**Read.**
- Revisited runs longer for almost everyone.
- Both lines drift down a little (fatigue, or getting used to the 300-character floor).
- This is the descriptive length pattern. Whether IC still moves after length is RQ1’s length-adjusted model, not this figure.

---

## 6. Flags

22 flags in 820 comments (2.7%). Too sparse for a “flag rate by role” chart. Table only.

| role | n | n flagged | % |
| --- | --- | --- | --- |
| Charitable Reader | 144 | 2 | 1.4 |
| Steelmanner | 144 | 3 | 2.1 |
| Perspective Shifter | 120 | 1 | 0.8 |
| Historian | 72 | 4 | 5.6 |
| Warrant Surfacer | 100 | 2 | 2.0 |
| Empiricist | 80 | 6 | 7.5 |
| Frame Skeptic | 90 | 3 | 3.3 |
| Conceptual Clarifier | 70 | 1 | 1.4 |

**Audit of the 22** (two researchers vs outside sources):

| sort | n |
| --- | ---: |
| Genuine error | 7 |
| Defensible but debatable | 9 |
| Plain disagreement | 6 |

Coder agreement: **18 / 22** (82%). Disagreements: 3 genuine vs debatable, 1 debatable vs disagreement. The table *is* the result.

Empiricist and Historian carry more flags — they make more checkable claims. That is a role pattern worth a sentence, not a bar chart of 1–6.

---

## 7. Habit change and trust

Same visual as RQ2 overall experience: dots = people, diamond = mean ± 1 SD, dashed line at 4. **Do not average** the three habit items or the two trust items.

![Habit change and trust](./img/06_habits_and_trust.png)

| item | mean | SD | n below 4 | n = 4 | n above 4 |
| --- | --- | --- | --- | --- | --- |
| Pausing before reacting | 4.8 | 1.3 | 4 | 6 | 14 |
| Questioning claims more | 5.1 | 1.1 | 1 | 6 | 17 |
| Changed how I reply | 3.8 | 1.4 | 8 | 10 | 6 |
| Trusted factual claims | 5.2 | 1.0 | 1 | 6 | 17 |
| Noticed agents' mistakes | 3.2 | 1.2 | 14 | 7 | 3 |

**Person-level values plotted as dots:**

| participant_id | pause | question claims | changed replies | trusted claims | noticed mistakes |
| --- | --- | --- | --- | --- | --- |
| 1 | 5 | 5 | 4 | 5 | 4 |
| 2 | 6 | 6 | 2 | 5 | 5 |
| 3 | 5 | 7 | 4 | 7 | 2 |
| 4 | 5 | 7 | 4 | 4 | 1 |
| 5 | 6 | 5 | 5 | 6 | 3 |
| 6 | 3 | 5 | 3 | 6 | 2 |
| 7 | 7 | 6 | 4 | 5 | 3 |
| 8 | 5 | 4 | 1 | 3 | 4 |
| 9 | 4 | 4 | 4 | 4 | 4 |
| 10 | 4 | 5 | 6 | 5 | 4 |
| 11 | 4 | 4 | 2 | 6 | 5 |
| 12 | 5 | 5 | 3 | 6 | 3 |
| 13 | 5 | 5 | 4 | 5 | 1 |
| 14 | 6 | 7 | 3 | 6 | 3 |
| 15 | 4 | 4 | 4 | 4 | 3 |
| 16 | 3 | 5 | 4 | 6 | 3 |
| 17 | 4 | 5 | 4 | 5 | 4 |
| 18 | 2 | 6 | 6 | 6 | 3 |
| 19 | 5 | 6 | 1 | 7 | 1 |
| 20 | 6 | 5 | 4 | 6 | 5 |
| 21 | 6 | 4 | 5 | 4 | 4 |
| 22 | 3 | 3 | 3 | 5 | 2 |
| 23 | 4 | 4 | 6 | 4 | 3 |
| 24 | 7 | 6 | 6 | 4 | 4 |

**Read.**
- People slightly agree they pause and question more. Changing how they *reply* sits near the midpoint.
- Trust in claims is high; noticing mistakes is low — consistent with only 22 flags.
- Self-report, no baseline, sample already wanted to improve critical thinking. Treat as description, not transfer.

Open text + interview **Change**: quotes, not a graph. In this fake run, 11 people gave a concrete outside-study example; most of those had pause ≥ 5. Likert-high with no example = leave it in the text as a caveat. (4 people sat below 4 on pausing.)

---

## 8. Interview themes *(table, not a frequency bar)*

Reflexive TA. Counts in the last column are “how many transcripts this showed up in,” not a ranking of importance.

| theme | what it is | example (fake) | n |
| --- | --- | --- | --- |
| Soft tone opened the door | Tentative phrasing vs normal replies | “It didn’t feel like a dunk, so I actually read it.” | 14 |
| Soft tone felt evasive | Same style, opposite read | “Just say you disagree. The hedging was annoying.” | 7 |
| One comment that landed | A single voice shifted the take | “The warrant one — I hadn’t seen the leap.” | 12 |
| Voices didn’t stick | Saw the comments, didn’t remember the role | “I know there were several, but I couldn’t tell them apart afterwards.” | 9 |
| Facts vs thinking | Useful even when untrusted | “I didn’t believe the stat, but the question was fair.” | 8 |
| Outside the tab | Pause on a real feed | “Caught myself typing a reply, deleted it, sat with it.” | 11 |

**Read.** Tone split the room (opened vs evasive). “Didn’t notice” in Figure 1B shows up here as voices that didn’t stick, not as skipped comments. Habit items in Figure 6 have somewhere to live (outside the tab) instead of standing as a lonely Likert.

---

## Takeaway *(this fake run)*

- First two roles ate most of the **volume** (they applied every session); mix (🔄 / 🤷 as a **% of that role’s comments**) is a different story — Steelmanner high on both, Empiricist higher 🔄 *rate* than *count*, Frame Skeptic high 🤷.
- 🔄 got rarer across days; 🤷 did not.
- Revisited responses were longer; both drifted down a little.
- Flags were rare; when audited, most were not clean factual errors. Two researchers agreed on 18/22.
- Usefulness is high for voices people remember; several later voices didn’t stick at end-of-study, even though every comment had been shown.
- People report pausing/questioning more than changing how they reply.

---

### Figure index

- `img/01_usefulness_and_notice.png` — strip + diamond by role; didn’t-notice counts
- `img/02_reactions_counts_by_role.png` — clustered bars, **counts**, 4 reaction types, n comments on x
- `img/03_tagging_intensity.png` — 24 dots, % of comments tagged
- `img/04_reaction_rates_by_session.png` — 4 small multiples, mean % ± 1 SD, fit through the 6 means
- `img/05a_length_paired.png` — 24 paired initial vs revisited
- `img/05b_length_by_session.png` — two mean lines ± 1 SD
- `img/06_habits_and_trust.png` — 5 strips, midpoint at 4
