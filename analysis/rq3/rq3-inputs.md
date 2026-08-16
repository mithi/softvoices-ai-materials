## The tables

Comment log (reactions and flags)

- One row = one generated comment, for one person, in one session.
- Row count varies: not every role fires every session (an LLM judges which roles fit).
- **All generated comments are shown** before the revisited response can be written. `Load more` only paces them two at a time. There is no “never opened” comment. Do not store a `seen` flag.
- **One reaction per comment.** Switching 🤔 to 🔄 replaces it. Clearing it stores `none`. A person cannot have two reactions on the same comment.
- 🚩 is a separate 0/1. It can sit on top of a reaction (or on `none`).

```
TABLE: comments
------------------------------------------------
1. participant_id    (1–24) who
2. session_id        (1–6) which session
3. post_id           which post
4. role              which agent (session order below)
5. comment_id        which comment
6. reaction          none | raised_new | sit_with | shifted | didnt_land
7. flagged           0/1
------------------------------------------------
```

Role values, in **session order** (do not sort by “best”):

`charitable_reader` · `steelmanner` · `perspective_shifter` · `historian` · `warrant_surfacer` · `empiricist` · `frame_skeptic` · `conceptual_clarifier`

Reaction values:

| stored as       | button                         |
| --------------- | ------------------------------ |
| `none`          | no tag                         |
| `raised_new`    | 🔔 raised something new        |
| `sit_with`      | 🤔 worth sitting with          |
| `shifted`       | 🔄 shifted my view             |
| `didnt_land`    | 🤷 didn't land for me          |

Response length (same word counts as RQ1)

```
TABLE: length
(144 rows = 24 people × 6 sessions)
------------------------------------------------
1. participant_id    (1–24) who
2. session_id        (1–6) which session
3. initial_words     word count of the first response
4. revisited_words   word count of the second response
------------------------------------------------
```

End-of-study (once, per person)

- Role usefulness: `1–7` or `didnt_notice`. **`didnt_notice` is not a 1 and is not missing data.** Means use only the 1–7 ratings.
- `didnt_notice` is **recall / salience**, not “they skipped the comment.” They had to view every generated comment. Split (or at least caveat) two cases: the role **never fired** for that person vs it fired and they still don’t remember the voice.
- Habit items: keep as three scores. Do not average them.
- Trust items: keep as two scores. Do not average them, do not reverse-score.

```
TABLE: end_study
(24 rows = 1 per person)
------------------------------------------------
1. participant_id
2. usefulness_charitable_reader     1–7 or didnt_notice
3. usefulness_steelmanner           1–7 or didnt_notice
4. usefulness_perspective_shifter   1–7 or didnt_notice
5. usefulness_historian             1–7 or didnt_notice
6. usefulness_warrant_surfacer      1–7 or didnt_notice
7. usefulness_empiricist            1–7 or didnt_notice
8. usefulness_frame_skeptic         1–7 or didnt_notice
9. usefulness_conceptual_clarifier  1–7 or didnt_notice
10. helped_most                     open text (which agent + why)
11. helped_least                    open text (which agent + why)
12. habit_pause                     (1–7) pausing before reacting
13. habit_question                  (1–7) questioning claims more
14. habit_reply                     (1–7) changed how I reply
15. habit_what_changed              open text
16. trust_claims                    (1–7) trusted factual claims
17. noticed_mistakes                (1–7) noticed agents making mistakes
18. flag_description                open text
------------------------------------------------
```

Flag audit (after the study; one row per flagged comment)

```
TABLE: flag_audit
------------------------------------------------
1. comment_id
2. participant_id
3. session_id
4. role
5. coder1_sort       genuine_error | debatable | disagreement
6. coder2_sort       genuine_error | debatable | disagreement
7. resolved_sort     after discussion
------------------------------------------------
```

Interview themes (after reflexive TA; not a starting table)

```
TABLE: interview_themes
------------------------------------------------
1. theme_name
2. definition
3. example_quote
4. n_transcripts    how many people this showed up in (quiet count, not a poll)
------------------------------------------------
```

## Locked rules — set these BEFORE touching data

| Decision                         | Value                                      | Why                                                                                          |
| -------------------------------- | ------------------------------------------ | -------------------------------------------------------------------------------------------- |
| Reaction on a comment            | **exactly one** (`none` or one of the four) | Buttons replace each other. Never count 🔔 and 🔄 on the same comment.                       |
| Flag                             | **separate** from reaction                 | 🚩 can sit on a reaction. Do not treat flag as a fifth reaction in the clustered bar chart.  |
| Exposure                         | **every generated comment is shown**       | Revisit is locked until then. `Load more` is pacing, not dropout. No `seen` column.          |
| Denominator for role charts      | all comments in `comments`                 | Every row was on screen. Volume differences are how often the role *fired*, not skip rate.   |
| Role order in figures            | **session order** (above)                  | Differences may be the role or the order — not a ranking.                                    |
| `didnt_notice`                   | exclude from usefulness mean               | Recall, not skipped UI. Recoding it as 1 or as NA-then-impute is wrong.                      |
| Habit / trust items              | **do not average**                         | They measure different things (pause vs reply; trust vs catching errors).                    |
| Length                           | **word count**                             | Same as RQ1. The 300-character rule is just a scoring gate.                                  |
| Person vs comment                | rates: person first; counts: comments      | A few heavy taggers will own a raw count. Person-mean the % tagged / % 🔄, then average.     |

## What each output number means

| Number                         | Meaning                                                                                                                                                          |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Count**                      | How many comments (or people). Volume. Early roles look bigger if they *apply* more often, not because later ones were hidden.                                   |
| **% of comments**              | Count ÷ comments that role generated (all of which were shown). Mix, given how often the role fired. This is what “less common over time” means.                 |
| **% tagged**                   | Share of comments with `reaction ≠ none`.                                                                                                                        |
| **n didn’t notice**            | People who chose `didnt_notice` for that role (of 24). Not a usefulness score. Cross with whether the role ever fired for them.                                  |
| **Mean**                       | The average. For usefulness: only over people who gave 1–7.                                                                                                      |
| **SD** (std. dev.)             | Spread between people. Example: ~2/3 of participants sit within 1 SD of the mean. Big SD = people disagree a lot.                                                |
| **Slope**                      | Change *per session* in a person-averaged rate. `−1.1 pp / session` = that reaction’s share of comments drops about 1.1 percentage points each day.              |
| **% agree** (flag audit)       | How often the two researchers gave the same sort. Report this next to the genuine / debatable / disagreement counts.                                             |
| **n transcripts** (themes)     | How many interviews a theme showed up in. A quiet annotation, not a bar chart of “which theme won.”                                                              |
