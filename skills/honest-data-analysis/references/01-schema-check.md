# Step 1 - Schema check

Make the model prove it read the file before it computes anything. Run this first, every time, then stop and confirm the load looks right.

Paste verbatim into your AI tool, with the CSV attached:

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
