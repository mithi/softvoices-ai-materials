# 🚀 R code Example

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
  - So: _explain `ic_score` using `response_type`, and also account for `response_length`._
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

- Report **d on the raw model only** — the raw model _is_ RQ1 (the total effect), so it's the result whose _size_ matters. The other two models are just checks ("is it only length?", "does it survive a method change?"), so they get estimate + p. You _can_ add d to all three if a reviewer wants it.

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
- Your `post_id` is written as 1, 2, 3, 4, 5, 6. To R those _look_ like a numeric scale — without `factor()`, R would assume post 6 is "six times" post 1, or that the posts sit evenly spaced on a line. That's nonsense; the numbers are just name tags.
- (Side note: in the main models, `participant_id` and `post_id` inside `(1 | ...)` are automatically treated as groups, so you don't need `factor()` there. You only need it when a bare id sits on the fixed-effects side, like `+ factor(post_id)`.)
