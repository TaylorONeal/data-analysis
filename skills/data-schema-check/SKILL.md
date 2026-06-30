---
name: data-schema-check
description: Use when running a schema or integrity check on an unfamiliar CSV before any analysis, so the model proves it read the file before it computes anything.
---

# Schema check

Run this first, every time. It forces the model to describe the file (columns, types, row count, date range, missing values) and stop. If it cannot describe the file, every number it gives you next is a guess.

Paste this prompt into your AI tool (Claude, ChatGPT, Gemini) with the CSV attached:

```text
You are a careful data analyst. I am uploading a CSV file. Before any analysis, do the following and stop.

STRICT RULES (apply to every response in this thread):
1. Use ONLY values that appear in the uploaded file. Never invent rows, dates, names, or numbers.
2. If a question cannot be answered from the file, reply "Not answerable from the data" and explain what is missing. Do not estimate.
3. When you state any number, cite the source: row indices used, column name, and the formula or aggregation.
4. When uncertain, say "uncertain" and explain why. Do not round into false precision.
5. Never extrapolate beyond the date range in the file.

TASK:
A. List every column name exactly as it appears, with the inferred data type (date, integer, float, text, categorical).
B. Report the row count, date range (min and max date), and the number of missing values per column.
C. Flag any data quality issues: duplicate rows, mixed timezones, inconsistent text casing, suspicious zero values, columns where the type is mixed.
D. Show the first 3 rows verbatim so I can confirm the load looks right.

Do NOT analyze yet. After you finish A through D, wait for my next prompt.
```

The model lists columns A-D and waits. Do not let it analyze yet. Once the load looks right, move to `data-analyze-honestly`.

Source: this prompt is lifted verbatim from the AI Data Analysis Playbook at https://thinkermetrics.com/ai-data-analysis. Do not edit the prompt body; it is battle-tested.
