# People or HR Analyst
*HRIS exports, engagement surveys, headcount and attrition*

> **Template stub.** This role is not yet in the canonical `data.ts` ROLES data, so the "what good output looks like" numbers below are intentionally left blank. The structure and the domain gotcha are real. Fill the Claim / Evidence / Calculation / Confidence with figures computed from your own file. Do not invent them; that is the one thing this whole repo exists to prevent.

## Plug into the prompt

- **Data sources:** HRIS export (Workday, BambooHR), survey CSV, ATS pipeline, comp bands.
- **Primary metric column:** Attrition %, time-to-fill, engagement score, comp ratio, headcount delta.
- **Grouping column:** Department, level, tenure band, manager, location.
- **Time grain:** Monthly for headcount and attrition. Per-survey-wave for engagement.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** _(one specific sentence with a number, computed from your data)_
- **Evidence:** _(source rows, column, aggregation)_
- **Calculation:** _(the actual math)_
- **Confidence:** _(high / medium / low, with sample size and a one-line reason)_

See `roles/marketing.md` for a filled-in example of this block.

## Watch out for

Small-n re-identification (PII). Any group with n < 5 can de-anonymize an individual. Tell the model to suppress and refuse to report any subgroup under 5, and never echo names or employee IDs.

---
Want this role promoted to a full overlay? See `CONTRIBUTING.md`.
