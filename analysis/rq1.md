# RQ1 Analysis Cheatsheet

**Question:** Is reading the agents' comments associated with increased Integrative Complexity (IC) from the *initial* response to the *revisited* response?

**IC** = a 1–7 score for how complex/balanced someone's reasoning is. Higher = more sides considered and connected.

**Contents** 
1. 🚀 Before you start 
2. 🚀 Pseudocode
3. 🚀 Reading the results  
4. 🚀 R code

# 🚀 1. Before you start

## The whole job in 7 steps

1. Put data in long format → 288 rows.
2. Check rater agreement (weighted kappa). Pass → continue. Fail → retrain raters, re-score.
3. Resolve rater disagreements → one final `ic_score` per response.
4. **Model 1 (raw):** the total IC difference.
5. **Model 2 (length-adjusted):** the IC difference *for the same amount of writing*.
6. **Model 3 (sensitivity):** re-run with posts as fixed effects. Does it still hold?
7. Report all three side by side.


## Locked decisions — set these BEFORE touching data

| Decision | Value | Why |
|---|---|---|
| `response_length` | **word count** | Word count, not characters — the 300-char rule is just a scoring gate. Controls for "just wrote more." |
| Kappa pass mark | **≥ 0.70** | Below this = raters don't agree enough. Pre-register your exact number. |
| Reference level | `initial` | Makes a **positive** coefficient mean "revisited scored higher." |
| Significance line | `p < .05` | Standard cutoff. |


## What each output number means

| Number | Plain English |
|---|---|
| **Estimate** (coefficient) | The IC gap, in IC points. `+0.62` = revisited scored 0.62 higher on the 1–7 scale. |
| **SE** (std. error) | How shaky the estimate is. Smaller = more precise. |
| **t value** | Estimate ÷ SE. Further from 0 = stronger signal. |
| **p value** | Chance of seeing a gap this big if the true gap were zero. `< .05` = unlikely to be a fluke. |
| **Cohen's d** | Size of the effect, in standard units. Ignores sample size. **0.2 small, 0.5 medium, 0.8 large.** Answers "is it big enough to care?" |



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

**On "own baseline" / `separate_out:`** each person gets their own baseline so the model judges them against themselves — did *their* revisited beat *their* initial, not whether person A beats person B. Why it matters: if Person A naturally writes at IC 5 and Person B at IC 2, lumping everyone together adds noise that muddies the initial-vs-revisited signal. Giving each person a separate starting level sets that difference aside. (`separate_out:` means "take these out of the picture." or *accounting for and setting aside*. Separate out the baselines) Same logic for posts.


## Step 4 — Model 2: Length-adjusted

**Need:** same as Model 1, **plus** `response_length`.

**Does:** the same thing, but now asks — *does IC still go up even between responses of the same length?*

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

- **Random** (Model 1): treats your 6 posts as a small sample standing in for *all possible posts* — a claim about posts in general.
- **Fixed** (Model 3): treats your 6 posts as *just these 6* — it measures the initial-vs-revisited gap *inside each post*, then combines. No claim beyond them.
- Reading the two estimates: **+0.62 (raw)** = across everything, revisited scored 0.62 higher on average. **+0.74 (sensitivity)** = within the same post, the gap is 0.74. Close together → robust; the method change barely moved the answer.
- If raw were **much higher** than sensitivity: part of the "effect" was really differences *between* posts leaking in, not revisiting. Weaker.
- If raw were **much lower** than sensitivity: post-to-post differences were *hiding* a real effect that shows once you control for them.

# 🚀 3. Reading the results

## Final report — put the three side by side

📝 **NOTE:** 
```
RAW              +0.62   p = .002    d = 0.38
LENGTH-ADJUSTED  +0.38   p = .041
SENSITIVITY      +0.74   p < .001
```


## Decision table — what the combination means

| Model 1 (raw) | Model 2 (length-adj) | Verdict |
|---|---|---|
| significant `+` | still significant `+` | **Strong support.** IC gain is real and not just longer writing. |
| significant `+` | shrinks, still significant | **Support, partly length.** Some gain is writing more; a real effect remains. |
| significant `+` | drops to ~0, not significant | **Weak.** The IC bump was mostly writing more. |
| not significant | — | **No evidence** of an IC change. |

Then Model 3 is the tie-breaker on trust: if it agrees with Model 1, you're solid. (`+` means positive `estimate`)

Recall: **"Significant" always means `p < .05`.** Nothing else. It means "probably not luck." It does *not* mean big or important — that's what Cohen's d is for.


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


# 🚀 4. R code

**How to read this section.** Four kinds of block, always labeled:

- 🟩 **RUN THIS** = real R code. Paste it into R.
- 🖥️ **WHAT R PRINTS** = a copy of what shows up on your screen after you run it.
- 📝 **NOTE** (plain text, outside any block) = numbers explained. Not printed by R.
- 📚 **Terms and syntax** = the R grammar, explained.


## Setup

🟩 RUN THIS
```r

# --- Packages ---
library(lme4)         # mixed models: lmer()
library(lmerTest)     # adds p-values to lmer() output (load AFTER lme4)
library(psych)        # cohen.kappa() for rater agreement
library(effectsize)   # t_to_d() for Cohen's d

# --- Load data ---
# Your CSV's header row must have these exact column names:
#   participant_id, post_id, response_type,
#   rater1_ic_score, rater2_ic_score, response_length
df <- read.csv("data.csv")   # "df" is just a nickname for your whole table

# If you only have raw text and need word count:
# df$response_length <- lengths(strsplit(df$response_text, "\\s+"))

# Make "initial" the reference level.
# => a POSITIVE estimate means revisited scored HIGHER.
df$response_type <- factor(df$response_type,
                           levels = c("initial", "revisited"))
```
📚 **Terms and syntax**
- **`df`** is your whole table. `df <- read.csv("data.csv")` loads the spreadsheet into that nickname. (You could call it anything; "df" = "data frame" = table.)
- **The column headers in your CSV are the names.** `df$response_type` means "the column literally named `response_type` inside `df`." The `$` = "reach into this table, grab that column."
- **Names in the code must match your CSV headers exactly**. `ResponseType` in the file ≠ `response_type` in the code.


## Step 1 — Rater agreement (weighted kappa)
🟩 RUN THIS

```r
kappa_out <- psych::cohen.kappa(
  cbind(df$rater1_ic_score, df$rater2_ic_score)
)
kappa_out$weighted.kappa   # read THIS number
```
📚 **Terms and syntax**
- `cbind(df$rater1_ic_score, df$rater2_ic_score)` glues the two raters' score columns side by side into a two-column table — the shape `cohen.kappa()` wants (each row = one response, column 1 = rater 1, column 2 = rater 2).
  - ("Bind" = join; "c" = column → "column bind". There's a matching `rbind` for rows.)

🖥️ **WHAT R PRINTS**
```
                 lower estimate upper
unweighted kappa  0.58     0.67  0.76
weighted kappa    0.71     0.78  0.85
```

📝 **NOTE:** weighted kappa = 0.78. That's above your 0.70 pass mark → raters agree enough → proceed.


## Step 2 — Final IC score

📝 **NOTE:** No model here. After raters resolve disagreements, make one agreed column, `df$ic_score`, and use it from now on. (If the two raters always matched, `ic_score` just equals `rater1_ic_score`.)


## Step 3 — Model 1: Raw (total effect)

🟩 RUN THIS

```r
model_raw <- lmer(
  ic_score ~ response_type + (1 | participant_id) + (1 | post_id),
  data = df
)
summary(model_raw)

# Cohen's d for the response_type effect:
ft     <- summary(model_raw)$coefficients
t_val  <- ft["response_typerevisited", "t value"]
df_val <- ft["response_typerevisited", "df"]
t_to_d(t_val, df_val)
```
📚 **Terms and syntax**
- In `lmer(..., data = df)`, the `data = df` part tells R "all these names live in the `df` table," so it looks them up as columns there.
- `ic_score ~ response_type + response_length`
  - Read `~` as **"explain … using …"**.
  - Read `+` as **"and also account for"**.
  - So: *explain `ic_score` using `response_type`, and also account for `response_length`.*
- `(1 | participant_id)` and `(1 | post_id)`
  - The general pattern is (`what_varies | across_what`). Here `1` (the baseline) varies across `participant_id`. `1` is R's code for the baseline / intercept — not the number one.
- `$coefficients` is a small table (a grid of numbers): one row per predictor, columns `Estimate`, `Std. Error`, `df`, `t value`, `Pr(>|t|)`. `$` reaches inside the `summary()` result to grab it (like `.coefficients` in other languages).
- `ft["response_typerevisited", "t value"]` = grid lookup by name: `[which row, which column]` → the one cell where they meet.

🖥️ **WHAT R PRINTS** (from `summary(model_raw)`)
```
Random effects:
 Groups         Name        Variance Std.Dev.
 participant_id (Intercept) 0.451    0.672
 post_id        (Intercept) 0.128    0.358
 Residual                   0.812    0.901
Number of obs: 288, groups: participant_id, 24; post_id, 6

Fixed effects:
                       Estimate Std. Error      df t value Pr(>|t|)
(Intercept)              3.1050     0.1980  27.410  15.682  < 2e-16 ***
response_typerevisited   0.6200     0.1990 263.10    3.116  0.00203 **
```

📚 **Terms and syntax**
- **`Pr(>|t|)` = the p-value.** That's just R's label for it. When you write it up, say "p = .002".
- **`df` in the output = degrees of freedom.** A technical input to the p-value; ignore it. (Different from the table nicknamed `df` — same letters, unrelated.)

🖥️ **WHAT R PRINTS** (from `t_to_d(...)`)
```
d    |       95% CI
-------------------
0.38 | [0.14, 0.63]
```

📚 **Terms and syntax**
- Report **d on the raw model only** — the raw model *is* RQ1 (the total effect), so it's the result whose *size* matters. The other two models are just checks ("is it only length?", "does it survive a method change?"), so they get estimate + p. You *can* add d to all three if a reviewer wants it.

📝 **NOTE:** Read the `response_typerevisited` row. Revisited is **+0.62 IC points** higher (Estimate), **p = .002** (the `Pr(>|t|)` column), and **d = 0.38**. Real effect, small-to-medium size.


## Step 4 — Model 2: Length-adjusted

🟩 RUN THIS
```r
model_adj <- lmer(
  ic_score ~ response_type + response_length +
             (1 | participant_id) + (1 | post_id),
  data = df
)
summary(model_adj)

ft2 <- summary(model_adj)$coefficients
t_to_d(ft2["response_typerevisited", "t value"],
       ft2["response_typerevisited", "df"])
```

🖥️ **WHAT R PRINTS** (fixed-effects rows only)
```
                       Estimate Std. Error      df t value Pr(>|t|)
response_typerevisited   0.3800     0.1850 261.40    2.054   0.0410 *
response_length          0.0040     0.0012 280.10    3.333   0.0010 **
```

📝 **NOTE:** The revisited estimate shrank from `0.62` (Model 1, raw) to `0.38`, but it's still significant (`p = .041`). Some of the gain was writing more — but a real effect remains after holding length steady.


## Step 5 — Model 3: Sensitivity (posts as fixed effects)

🟩 RUN THIS
```r
model_fixedpost <- lmer(
  ic_score ~ response_type + factor(post_id) + (1 | participant_id),
  data = df
)
summary(model_fixedpost)
```

🖥️ **WHAT R PRINTS** (`response_type` row only)
```
                       Estimate Std. Error      df t value Pr(>|t|)
response_typerevisited   0.7400     0.1600 258.00   4.625  < .001 ***
```

📝 **NOTE:** Still strongly positive (+0.74), close to Model 1's +0.62. The result doesn't depend on how posts were handled → robust.

📚 **Terms and syntax**
- `factor()` tells R "treat this column as labels, not numbers." These are six separate categories — no order, no spacing. The model estimates a separate effect for each post instead of fitting one straight-line "post number" trend.
- Your `post_id` is written as 1, 2, 3, 4, 5, 6. To R those *look* like a numeric scale — without `factor()`, R would assume post 6 is "six times" post 1, or that the posts sit evenly spaced on a line. That's nonsense; the numbers are just name tags.
- (Side note: in the main models, `participant_id` and `post_id` inside `(1 | ...)` are automatically treated as groups, so you don't need `factor()` there. You only need it when a bare id sits on the fixed-effects side, like `+ factor(post_id)`.)


