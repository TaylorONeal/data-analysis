# SaaS Growth Analyst
*Stripe, HubSpot, product analytics, billing exports*

## Plug into the prompt

- **Data sources:** Stripe revenue export, HubSpot pipeline CSV, ProfitWell, Stripe Sigma.
- **Primary metric column:** MRR, ARR, NRR, gross churn %, LTV:CAC, trial-to-paid conversion, expansion revenue.
- **Grouping column:** Plan tier, acquisition channel, cohort month, company size band.
- **Time grain:** Monthly for revenue. Weekly for trial conversion.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** Self-serve trials converted at 14.2% vs 22.1% for sales-assisted in Q1, but at 1/8th the CAC.
- **Evidence:** Rows 211 to 498, acquisition_channel, converted_flag, cac_cents.
- **Calculation:** Self-serve: 1,142 / 8,042 = 14.2%, mean CAC = $47. Sales: 218 / 986 = 22.1%, mean CAC = $384. CAC ratio = 8.17.
- **Confidence:** High. n=9,028 trials, full quarter.

## Watch out for

Cohorts mid-conversion. Exclude any cohort younger than the trial length.

---
Lifted verbatim from the ROLES data in the AI Data Analysis Playbook: https://thinkermetrics.com/ai-data-analysis
