# Marketing Campaign Manager
*Meta Ads, email, paid social*

## Plug into the prompt

- **Data sources:** Meta Ads Manager export, ConvertKit campaigns, Google Sheets pivots
- **Primary metric column:** ROAS, CPA, CTR, conversion rate. For email: open, click, unsubscribe.
- **Grouping column:** Ad creative (image, video, carousel), audience segment, placement, subject-line variant.
- **Time grain:** Daily for paid. Per-send for email.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** Video creatives delivered 1.8x lower CPA than static across $24,140 spend, April 1 to 28.
- **Evidence:** Rows 12 to 186, ad_format column, CPA = spend / conversions per row.
- **Calculation:** Video CPA = $5,200 / 412 = $12.62. Static CPA = $18,940 / 834 = $22.71. Ratio = 1.80.
- **Confidence:** High. n=412 video conversions, n=834 static. Same audience, same dates.

## Watch out for

Attribution windows that overlap. Tell the model to cite the window in every claim.

---
Lifted verbatim from the ROLES data in the AI Data Analysis Playbook: https://thinkermetrics.com/ai-data-analysis
