# Product or App Analyst
*Mixpanel, Amplitude, Heap, in-house event data*

## Plug into the prompt

- **Data sources:** Event export (CSV or SQL dump), Mixpanel, Amplitude, Heap, Pendo, cohort tables.
- **Primary metric column:** DAU/MAU, day-7 / day-30 retention, activation rate, funnel conversion, feature adoption %.
- **Grouping column:** Signup cohort week, platform (iOS, Android, web), feature flag or A/B variant (Optimizely, Adobe Target), user persona.
- **Time grain:** Cohort week for retention. Daily for engagement.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** Day-7 retention dropped from 42% to 31% for the cohort that signed up the week of March 3.
- **Evidence:** Rows 78 to 104, cohort_week column, retained_d7 / cohort_size.
- **Calculation:** Feb 24 cohort: 1,840 / 4,381 = 42.0%. Mar 3 cohort: 1,289 / 4,158 = 31.0%. Delta = -11 pts.
- **Confidence:** Medium. Drop coincides with onboarding redesign ship date 3/2. HYPOTHESIS: redesign regressed activation.

## Watch out for

Counting users vs sessions. Have the model restate which entity it's counting in every claim.

---
Lifted verbatim from the ROLES data in the AI Data Analysis Playbook: https://thinkermetrics.com/ai-data-analysis
