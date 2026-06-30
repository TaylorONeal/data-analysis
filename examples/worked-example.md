# Worked example: paid-social ad performance

This is a full pass of the four-step workflow against `sample-data.csv` (48 rows, daily paid-social ad performance for April 2026). Every number below was computed from the file. If you run the same prompts on the same CSV you should land on the same figures, give or take how your tool rounds.

The point is not the dataset. It is the shape of the output: a claim, the rows behind it, the math, and a confidence level you can argue with.

---

## Step 1 - Schema check

Prompt used: `references/01-schema-check.md` (or the `data-schema-check` skill). The model is told to describe the file and stop.

**A. Columns and inferred types**

| Column | Type |
| --- | --- |
| `row_id` | integer |
| `date` | date |
| `ad_format` | categorical |
| `audience` | categorical |
| `spend` | float |
| `impressions` | integer |
| `clicks` | integer |
| `conversions` | integer |

**B. Shape**

- Row count: 48
- Date range: 2026-04-01 to 2026-04-19
- Missing values per column: row_id=0, date=0, ad_format=0, audience=0, spend=0, impressions=0, clicks=0, conversions=0 (none)

**C. Data quality flags**
- `ad_format` is clean categorical with 3 values: carousel, static, video.
- No duplicate `row_id`. No mixed casing in text columns. No negative spend.
- `conversions` includes legitimate zero-ish low days; not treated as missing.

**D. First 3 rows verbatim**

| row_id | date | ad_format | audience | spend | impressions | clicks | conversions |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 2026-04-01 | video | retargeting | 679.76 | 31840 | 760 | 68 |
| 2 | 2026-04-01 | static | prospecting | 310.59 | 25667 | 292 | 9 |
| 3 | 2026-04-01 | carousel | retargeting | 637.41 | 35889 | 636 | 38 |

The model stops here and waits. No analysis yet.

---

## Step 2 - Analyze

Prompt used: `references/02-analyze.md` (or `data-analyze-honestly`). Restated back first: PRIMARY METRIC = CPA (`spend / conversions`). GROUPING COLUMN = `ad_format`.

### Part B - category ranking (CPA, lower is better)

| ad_format | n rows | spend | conversions | CPA |
| --- | --- | --- | --- | --- |
| video | 16 | $12,799.34 | 1127 | $11.36 |
| carousel | 16 | $8,191.44 | 465 | $17.62 |
| static | 16 | $5,735.08 | 166 | $34.55 |

**Claim:** `video` delivered the lowest CPA at $11.36, 3.04x cheaper than `static` at $34.55.
**Evidence:** all 48 rows, grouped on `ad_format`; CPA = sum(spend) / sum(conversions) per group.
**Calculation:** video = $12,799.34 / 1127 = $11.36. static = $5,735.08 / 166 = $34.55. Ratio = 34.55 / 11.36 = 3.04.
**Confidence:** High. n=1127 video conversions and n=166 static conversions across the full 2026-04-01 to 2026-04-19 window.

One example row from each group:

- video: row 1 (2026-04-01), spend $679.76, conversions 68, CPA $10.00.
- static: row 2 (2026-04-01), spend $310.59, conversions 9, CPA $34.51.

### Part A - time patterns

- Highest conversion day: **2026-04-12** with 201 conversions across all formats.
- Lowest conversion day: **2026-04-02** with 33 conversions.
- The 2026-04-12 spike shows up in the raw rows for that date (a deliberate bump in the sample data), not an artifact of aggregation.

### Part C - self-consistency check

Pooled CPA for `video` (sum spend / sum conversions) = $11.36. Recomputed a second way as the mean of per-row CPA across 16 video rows with conversions > 0 = $11.32. The two differ because per-row mean weights small-volume days equally; the pooled number is the one to cite. Flag, not a tiebreaker.

### Part D - gaps

1. No revenue or order-value column, so CPA cannot become ROAS from this file alone.
2. No creative-level IDs, so 'video wins' cannot be attributed to a specific asset.
3. Attribution window is not encoded; same-day vs 7-day conversions are indistinguishable here.

---

## Step 3 - Visualize

Prompt used: `references/03-visualize.md` (or `data-chart-specs`). Specs, not rendered images.

**Chart 1 - CPA by ad format (bar)**
- X: `ad_format` (3 categories). Y: CPA in dollars, include zero.
- Title: "Video ran 3.0x cheaper per conversion than static across $26,726 spend, Apr 1-19"
- Focal number: $11.36 vs $34.55. Annotate both bars with their CPA.
- Rows: all 48, grouped on `ad_format`.

**Chart 2 - conversions per day (line)**
- X: `date` (2026-04-01 to 2026-04-19). Y: daily conversions, include zero.
- Title: "Conversions peaked at 201 on 2026-04-12"
- Annotations: peak point (2026-04-12, 201) and low point (2026-04-02, 33).

**Chart 3 - spend vs conversions by format (scatter)** - chosen to show efficiency, not just volume.
- X: spend per row. Y: conversions per row. Color: `ad_format`. Steeper slope = cheaper conversions.

---

## Step 4 - Insight brief

Prompt used: `references/04-insight-brief.md` (or `data-insight-brief`).

**Chart 1 brief**
1. THE INSIGHT: `video` converted at $11.36 CPA vs $34.55 for `static`, a 3.04x gap across 48 rows, Apr 1-19.
2. WHY IT MATTERS: CPA is the efficiency lever on acquisition cost; a 3x gap is budget being left on the table.
3. DATA CONNECTION: 1127 video conversions on $12,799.34 spend; 166 static conversions on $5,735.08 spend. Full sample, n=48 rows.
4. NEXT STEPS: shift a fixed slice of `static` budget into `video` for a two-week test on matched audiences, hold creative count constant, target CPA at or below $13.63 to call it.

**Chart 2 brief**
1. THE INSIGHT: conversions peaked at 201 on 2026-04-12, 2.2x the daily average of 93.
2. WHY IT MATTERS: a single-day spike that is real (not a tracking glitch) is worth replicating; if it is a glitch, it is worth killing before it skews the month.
3. DATA CONNECTION: daily totals across 19 days; peak 2026-04-12=201, low 2026-04-02=33.
4. NEXT STEPS: pull the creative and audience live on the peak date, confirm spend was not simply 1.6x higher, decide replicate vs discard.

---

## What to copy from this

Notice what the model never did: it never gave a number without a row range, never said "performance was strong," never invented a column. When a question could not be answered from the file (revenue, creative ID, attribution window) it said so in Part D instead of guessing. That is the whole game.
