---
name: data-analyze-honestly
description: Use when finding time patterns and ranking categories in a CSV and every finding must be cited with source rows, the math shown, and confidence stated.
---

# Analyze honestly

Run this after the schema check, in the same chat. It locks every finding into Claim / Evidence / Calculation / Confidence and bans vague qualifiers.

Paste this prompt into your AI tool (Claude, ChatGPT, Gemini) with the CSV attached:

```text
Continuing from the same file. Same strict rules apply: ground every answer in the data, cite source rows, say "Not answerable from the data" when it isn't there. Do not extrapolate beyond the date range.

TASK: Find time-based patterns AND rank categories, in one pass.

Before you begin, restate two things back to me:
- PRIMARY METRIC: the column you will treat as the headline number.
- GROUPING COLUMN: the column you will rank by.
If either is ambiguous, ask. Do not assume.

OUTPUT FORMAT - use this structure for every finding:
- Claim: one sentence, specific
- Evidence: rows used (e.g. rows 12 to 18), column, aggregation
- Calculation: the actual math (e.g. "sum of [primary metric] rows 12-18 = 4,210; prior period = 1,450; change = +190%")
- Confidence: high / medium / low, and why

PART A - TIME PATTERNS
1. Highest period for the primary metric (which week or day, exact total, what records drove it)
2. Lowest period
3. Largest period-over-period percentage change, both up and down
4. Any sustained trend (3+ consecutive periods moving in the same direction)
5. Any anomaly that breaks the trend, with a one-line cause hypothesis (label it HYPOTHESIS)

PART B - CATEGORY RANKING
First, list the categories present in the grouping column. Use only values that appear in the data. If there is no clean grouping column, infer one ONLY when you can state the rule explicitly. State the rule. If you cannot infer categories, stop and say so.

Then rank by:
- Mean of the primary metric per record
- Median of the primary metric per record
- Sample size (n=) per category. Flag any category with n < 5 as low-confidence.

For the top category vs the bottom category, give:
- Concrete ratio (e.g. "Category A averaged 2.3x Category B on the primary metric")
- One example record from each (cite row index)
- Two specific observable differences between the two example records

PART C - SELF-CONSISTENCY CHECK
Recompute the headline number from Part B a second way (if you used mean, also try total of the primary metric per category divided by total records per category). If the two methods disagree, report both and explain.

PART D - GAPS
List 3 things you cannot determine from this data alone and what additional data would resolve them.

Do not use vague qualifiers like "strong," "mixed," "notable," "performing well." Every finding needs a specific number.
```

Expect a restated primary metric and grouping column first. If the model assumes either instead of asking, send it back. Then move to `data-chart-specs`.

Source: this prompt is lifted verbatim from the AI Data Analysis Playbook at https://thinkermetrics.com/ai-data-analysis. Do not edit the prompt body; it is battle-tested.
