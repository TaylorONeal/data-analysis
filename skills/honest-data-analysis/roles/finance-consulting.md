# Consultant or Financial Analyst
*Client P&Ls, segment revenue, board-deck inputs*

## Plug into the prompt

- **Data sources:** P&L exports, segment revenue files, GL extracts, market-sizing inputs.
- **Primary metric column:** Revenue growth %, gross margin %, contribution margin, EBITDA, burn rate, runway months.
- **Grouping column:** Business unit, product line, customer segment, region, sales rep.
- **Time grain:** Monthly close, with QoQ and YoY comparisons.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** Enterprise segment grew 34% QoQ in Q1, but gross margin compressed from 62% to 54%.
- **Evidence:** Rows 14 to 29, segment = "Enterprise", revenue, cogs.
- **Calculation:** Q4 Enterprise revenue = $4.12M, GM = 62%. Q1 = $5.52M, GM = 54%. Growth = +34.0%. Margin delta = -8 pts.
- **Confidence:** High at segment level. Cause of margin compression needs COGS breakdown.

## Watch out for

Currency mixing and restated periods. Flag any row where currency or period_status changes.

---
Lifted verbatim from the ROLES data in the AI Data Analysis Playbook: https://thinkermetrics.com/ai-data-analysis
