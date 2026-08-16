# RQ2 Analysis Cheatsheet

# 🚀 Pseudocode

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

- per_person_avg = each participant's mean of their 6 per-session ratings
- end_score = that participant's end-of-study score

---

**\*\***\***\*\*** END **\*\***\***\*\***
