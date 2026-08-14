# RQ2 Analysis Cheatsheet
**Question:** How do users experience the interface? (descriptive only)

**Contents**
1. 🚀 Before you start
2. 🚀 Pseudocode

---
# 🚀 1. Before you start

## The two tables

Per session (6 measures)
```
TABLE: per_session_table 
(144 rows = 24 people × 6 sessions)
------------------------------------------------
1. participant_id    (1–24) who
2. session_id        (1–6) which session
3. paas_effort       (1–9) total mental effort
4. germane           (1–7) effort felt productive
5. extraneous        (1–7) effort felt wasted 
6. effectiveness     (1–7) did help me reflect 
7. enjoyability      (1–7) did I enjoy it 
8. adoption          (1–7) would I keep using it 
------------------------------------------------
```
End-of-study (once, per person)
- One single Paas item for overall effort (1–9)
-  **Multi-item (3 each per measure)** - each will be averaged into one score
```
TABLE: end_study _table
(24 rows = 1 per person)
------------------------------------------------
1. participant_id
2. overall_paas_effort
3. productive_1
4. productive_2
5. productive_3
6. wasted_1
7. wasted_2
8. wasted_3
9. effectiveness_1
10. effectiveness_2
11. effectiveness_3
12. enjoyability_1
13. enjoyability_2
14. enjoyability_3
15. adoption_1
16. adoption_2
17. adoption_3
------------------------------------------------
```

## What each output number means
| Number | Meaning |
|---|---|
| **Mean** | The average rating |
| **SD** (std. dev.) | Spread between people. Example: ~2/3 of participants sit within 1 SD of the mean. Big SD = people disagree a lot. |
| **Cronbach's alpha** | For a multi-item scale: do the items move together? 0–1. **≥ .70 = yes**, safe to average them into one score. Below this, the items don't hang together — report it, don't silently average. |
| **r** (cross-check) | Correlation between the light per-session score and the fuller end-of-study score. Closer to 1 = the light rating tracked the full one. |
| **Slope** | Rating change *per session*. `+0.10` = drifts up ~0.1 points each session. `-` = drifts down (e.g., novelty fading). Lets one number say "rises / falls per session."|

---

# 🚀 2. Pseudocode


## Step 1. Summarize per-session measures

```
INPUT: per_session table (144 rows, 6 measures)

for each measure:
  compute mean, sd, min, max (144 rows)

for each measure:
  for each session: (6 sessions)
    - compute mean, sd, min, max per session 
      [24 participants, 6 outputs, 1 output per session]

    - compute slope = mixed_model(
      predict:      measure
      from:         session
      separate_out: each participant's own baseline
    )
```

## Step 2 — End-of-study: check consistency, average, summarize
```
INPUT: end_of_study_table (24 rows /participants)

FOR each multi-item scale (5 measures) per participant
    - compute alpha = cronbach(its 3 item columns)
    - IF alpha < 0.70: flag it, inspect the 3 items
    - scale_score mean(their 3 items) per participant

THEN FOR each end_study measure (the 5 scale_scores + overall_effort):
    - compute mean, SD (across 24 participants)
```

## Step 4 — Cross-check per-session vs end-of-study

```
INPUT: end_of_study_table

Pair each per-session column with its end-of-study scale_score (mean)
	
FOR each of the 6 pairs:
    - compute r = correlation(per_person_avg, end_score)  
	  (across the 24 participants)

```

Notes:
-  per_person_avg = each participant's mean of their 6 per-session ratings 
-  end_score = that participant's end-of-study score

---


************* END ************* 
