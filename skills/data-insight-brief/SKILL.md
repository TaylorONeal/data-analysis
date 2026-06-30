---
name: data-insight-brief
description: Use when turning chart findings into decision-ready insight briefs with a specific number, a business reason, the cited data, and one concrete next step.
---

# Insight brief

This turns each chart into a four-part brief: the insight, why it matters, the data connection, and one concrete next step. You can ship deck slides off this output and defend them.

Paste this prompt into your AI tool (Claude, ChatGPT, Gemini) with the CSV attached:

```text
For each visualization I describe below, write a four-part insight brief. Same strict rules: ground every claim in the data, cite rows, say "Not answerable from the data" when needed.

OUTPUT FORMAT (exactly this, for each chart):

1. THE INSIGHT (one sentence, specific number)
  - Bad: "Category A performed well."
  - Good: "Category A outperformed Category B by 2.3x on the primary metric across 47 records in March-April."

2. WHY IT MATTERS (one sentence connecting to a business goal)
  - Tie it to acquisition, retention, revenue, margin, awareness, or efficiency.
  - If you cannot tie it to a goal, say so.

3. DATA CONNECTION (cite the numbers)
  - Sample size, time range, the calculation, the source rows.
  - If the sample size is small (n < 30), flag it.

4. NEXT STEPS (one concrete action)
  - Bad: "Invest more in Category A."
  - Good: "Run a 4-week test allocating 50% of budget to Category A and 50% to Category B on matched audiences, measure the primary metric, target a 1.5x lift to declare significance."

Charts to write briefs for:
1. [PASTE CHART 1 DESCRIPTION + KEY NUMBERS]
2. [PASTE CHART 2 DESCRIPTION + KEY NUMBERS]
3. [PASTE CHART 3 DESCRIPTION + KEY NUMBERS]

Do not pad. If a section cannot be filled honestly, write "Cannot answer from this data" and move on.
```

Paste each chart description plus its key numbers where the prompt marks it. If a section cannot be filled honestly the model writes "Cannot answer from this data" and moves on.

Source: this prompt is lifted verbatim from the AI Data Analysis Playbook at https://thinkermetrics.com/ai-data-analysis. Do not edit the prompt body; it is battle-tested.
