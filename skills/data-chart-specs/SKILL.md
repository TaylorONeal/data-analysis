---
name: data-chart-specs
description: Use when you need publication-ready chart specifications (not rendered images) for a dataset you will build yourself in Tableau, Excel, or Looker.
---

# Chart specs

A spec is a contract you can audit. A rendered PNG from an AI is a guess wearing makeup. This prompt returns chart type, axes, encoding, titles, and exact annotation coordinates.

Paste this prompt into your AI tool (Claude, ChatGPT, Gemini) with the CSV attached:

```text
Continuing from the same file. Same strict rules.

TASK: Generate publication-ready chart specifications I can build in Tableau, Excel, or Looker. I want specs, not code, unless I ask.

For each of the 3 charts below, output:
1. Chart type (bar, line, scatter, area, etc.) and why this type
2. X axis: column name, label text, tick format
3. Y axis: column name, label text, tick format, whether to include zero
4. Series / color encoding (and the exact color hex codes if you suggest a palette)
5. Title (specific, not generic. Include the actual finding, e.g. "Category A delivered 2.3x the primary metric vs Category B, Mar-Apr")
6. Subtitle that gives context (sample size, date range, source)
7. The 1-2 annotations you would add (with exact data point coordinates)
8. The single number that should be the visual focal point

CHARTS:
1. Primary metric over time, with the highest and lowest periods annotated
2. Category performance comparison (use the rankings from the prior step)
3. ONE more chart you choose, based on what you found. Justify the pick in one sentence.

CONSTRAINTS:
- Do not suggest a pie chart unless there are exactly 2 or 3 categories
- Do not stack multiple metrics on one axis
- Every chart needs a clear "so what" in its title
- Cite the rows / aggregation used for each chart so I can rebuild it
```

Build the charts yourself against the real data. Then feed the chart descriptions into `data-insight-brief`.

Source: this prompt is lifted verbatim from the AI Data Analysis Playbook at https://thinkermetrics.com/ai-data-analysis. Do not edit the prompt body; it is battle-tested.
