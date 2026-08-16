# RQ1 Analysis Cheatsheet

**Question:** Is reading the agents' comments associated with increased Integrative Complexity (IC) from the _initial_ response to the _revisited_ response?

**IC** = a 1–7 score for how complex/balanced someone's reasoning is. Higher = more sides considered and connected.

**Contents**

1. 🚀 Before you start
2. 🚀 Pseudocode
3. 🚀 Reading the results

# 🚀 1. Before you start

## The whole job in 7 steps

1. Put data in long format → 288 rows.
2. Check rater agreement (weighted kappa). Pass → continue. Fail → retrain raters, re-score.
3. Resolve rater disagreements → one final `ic_score` per response.
4. **Model 1 (raw):** the total IC difference.
5. **Model 2 (length-adjusted):** the IC difference _for the same amount of writing_.
6. **Model 3 (sensitivity):** re-run with posts as fixed effects. Does it still hold?
7. Report all three side by side.

## Locked decisions — set these BEFORE touching data

| Decision          | Value          | Why                                                                                                    |
| ----------------- | -------------- | ------------------------------------------------------------------------------------------------------ |
| `response_length` | **word count** | Word count, not characters — the 300-char rule is just a scoring gate. Controls for "just wrote more." |
| Kappa pass mark   | **≥ 0.70**     | Below this = raters don't agree enough. Pre-register your exact number.                                |
| Reference level   | `initial`      | Makes a **positive** coefficient mean "revisited scored higher."                                       |
| Significance line | `p < .05`      | Standard cutoff.                                                                                       |

## What each output number means

| Number                     | Plain English                                                                                                                         |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Estimate** (coefficient) | The IC gap, in IC points. `+0.62` = revisited scored 0.62 higher on the 1–7 scale.                                                    |
| **SE** (std. error)        | How shaky the estimate is. Smaller = more precise.                                                                                    |
| **t value**                | Estimate ÷ SE. Further from 0 = stronger signal.                                                                                      |
| **p value**                | Chance of seeing a gap this big if the true gap were zero. `< .05` = unlikely to be a fluke.                                          |
| **Cohen's d**              | Size of the effect, in standard units. Ignores sample size. **0.2 small, 0.5 medium, 0.8 large.** Answers "is it big enough to care?" |

# 🚀 2. Pseudocode

## The data you start with

One row = one response. **288 rows** = 24 participants × 6 posts × 2 response types.

```
TABLE: responses
------------------------------------------------
participant_id    who wrote it (1–24)
post_id           which post (1–6)
response_type     "initial" or "revisited"
rater1_ic_score   rater 1's IC score (1–7)
rater2_ic_score   rater 2's IC score (1–7)
response_length   number of words
------------------------------------------------
```

## Step 1 — Check rater agreement

**Need:** the two raters' IC scores for every response. (`rater1_ic_score`, `rater2_ic_score`)

**Does:** measures how much the two raters agreed. "Weighted" = a 4-vs-5 disagreement counts as milder than a 4-vs-7. Unweighted counts only exact matches; weighted gives partial credit for near-misses. Use weighted (IC is an ordered 1–7 scale, so "close" should count).

**Get:** `kappa` (weighted) — one number, ~0 to 1. Higher = more agreement.

**Rule:**

```
IF kappa < 0.70:
    retrain the raters → re-score → check kappa again
ELSE:
    go to Step 2
```

## Step 2 — Resolve disagreements → final score

**Rule:**

```
FOR each response:
    IF rater1_score == rater2_score:
        ic_score = that score
    ELSE:
        raters discuss until they agree on one number → ic_score
```

Now every response has one `ic_score`. Use this from here on.

## Step 3 — Model 1: Raw (the total effect)

**Need:** `ic_score`, `response_type`, `participant_id`, `post_id`.

**Does:** finds the average IC gap between initial and revisited responses — while allowing that (a) some people are naturally deeper writers, and (b) some posts naturally pull deeper takes.

```
fit_mixed_model(
    predict:      ic_score
    from:         response_type
    separate_out: each participant has own baseline
                  each post has own baseline
)
```

**Get:** `estimate`, `SE`, `t`, `p`, `Cohen's d`

**Read:** the `estimate` = how many IC points higher revisited is, on average.

**On "own baseline" / `separate_out:`** each person gets their own baseline so the model judges them against themselves — did _their_ revisited beat _their_ initial, not whether person A beats person B. Why it matters: if Person A naturally writes at IC 5 and Person B at IC 2, lumping everyone together adds noise that muddies the initial-vs-revisited signal. Giving each person a separate starting level sets that difference aside. (`separate_out:` means "take these out of the picture." or _accounting for and setting aside_. Separate out the baselines) Same logic for posts.

## Step 4 — Model 2: Length-adjusted

**Need:** same as Model 1, **plus** `response_length`.

**Does:** the same thing, but now asks — _does IC still go up even between responses of the same length?_

```
fit_mixed_model(
    predict:      ic_score
    from:         response_type + response_length
    separate_out: each participant has own baseline
                  each post has own baseline
)
```

**Read:** compare this `estimate` to Model 1's.

- Stays about the same → the IC gain is **not** just writing more.
- Shrinks toward 0 → part of the gain **was** just writing more.
- Drops to ~0 → the gain was **mostly** writing more.

## Step 5 — Model 3: Sensitivity check (posts as fixed)

**Why:** there are only 6 posts — too few to treat as a "random sample" reliably. This re-runs the test treating each post as its own fixed thing, to check the result doesn't depend on that choice.

```
fit_mixed_model(
    predict:        ic_score
    from:           response_type + post_id
    separate_out:   each participant has own baseline
)
```

**Read:** if the `estimate` is close to Model 1's, the result is robust. If it flips or vanishes, flag it.

- **Random** (Model 1): treats your 6 posts as a small sample standing in for _all possible posts_ — a claim about posts in general.
- **Fixed** (Model 3): treats your 6 posts as _just these 6_ — it measures the initial-vs-revisited gap _inside each post_, then combines. No claim beyond them.
- Reading the two estimates: **+0.62 (raw)** = across everything, revisited scored 0.62 higher on average. **+0.74 (sensitivity)** = within the same post, the gap is 0.74. Close together → robust; the method change barely moved the answer.
- If raw were **much higher** than sensitivity: part of the "effect" was really differences _between_ posts leaking in, not revisiting. Weaker.
- If raw were **much lower** than sensitivity: post-to-post differences were _hiding_ a real effect that shows once you control for them.

# 🚀 3. Reading the results

## Final report — put the three side by side

📝 **NOTE:**

```
RAW              +0.62   p = .002    d = 0.38
LENGTH-ADJUSTED  +0.38   p = .041
SENSITIVITY      +0.74   p < .001
```

## Decision table — what the combination means

| Model 1 (raw)   | Model 2 (length-adj)         | Verdict                                                                       |
| --------------- | ---------------------------- | ----------------------------------------------------------------------------- |
| significant `+` | still significant `+`        | **Strong support.** IC gain is real and not just longer writing.              |
| significant `+` | shrinks, still significant   | **Support, partly length.** Some gain is writing more; a real effect remains. |
| significant `+` | drops to ~0, not significant | **Weak.** The IC bump was mostly writing more.                                |
| not significant | —                            | **No evidence** of an IC change.                                              |

Then Model 3 is the tie-breaker on trust: if it agrees with Model 1, you're solid. (`+` means positive `estimate`)

Recall: **"Significant" always means `p < .05`.** Nothing else. It means "probably not luck." It does _not_ mean big or important — that's what Cohen's d is for.

## Example outputs (4 cases)

**Case A — Real effect, survives length (supports RQ1)**

```
RAW              estimate = +0.62   p = .002    d = 0.38
LENGTH-ADJUSTED  estimate = +0.38   p = .04
```

> Revisited scored 0.62 IC points higher. After matching for length it's still +0.38 and significant. Some of the gain is writing more — but not all. **Supports RQ1.**

**Case B — Gain was mostly length (honest near-null)**

```
RAW              estimate = +0.55   p = .01     d = 0.32
LENGTH-ADJUSTED  estimate = +0.08   p = .60
```

> The raw bump vanishes once you match for length. The IC gain came from people writing more, not reasoning deeper. **Weak / no real effect.**

**Case C — Just noise**

```
RAW              estimate = +0.05   p = .78     d = 0.03
```

> Basically zero, and the p-value says it's easily luck. **No evidence for RQ1.** (No need to read Model 2 closely — there's nothing to explain.)

**Case D — Fully robust**

```
RAW              estimate = +0.78   p < .001    d = 0.55
LENGTH-ADJUSTED  estimate = +0.51   p = .008
SENSITIVITY      estimate = +0.74   p < .001
```

> Big medium-sized gain, holds after length adjustment, holds when posts are fixed. **Strong, robust support for RQ1.**
