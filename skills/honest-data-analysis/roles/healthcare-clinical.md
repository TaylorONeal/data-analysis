# Healthcare or Clinical Analyst
*EHR extracts, claims, quality-measure and outcomes data*

> **Template stub.** This role is not yet in the canonical `data.ts` ROLES data, so the "what good output looks like" numbers below are intentionally left blank. The structure and the domain gotcha are real. Fill the Claim / Evidence / Calculation / Confidence with figures computed from your own file. Do not invent them; that is the one thing this whole repo exists to prevent.

## Plug into the prompt

- **Data sources:** De-identified EHR extract, claims CSV, registry export, quality-measure file.
- **Primary metric column:** Readmission rate, length of stay, measure compliance %, cost per episode, outcome rate.
- **Grouping column:** Service line, provider, payer, diagnosis group, site.
- **Time grain:** Monthly close, with rolling 12-month comparisons.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** _(one specific sentence with a number, computed from your data)_
- **Evidence:** _(source rows, column, aggregation)_
- **Calculation:** _(the actual math)_
- **Confidence:** _(high / medium / low, with sample size and a one-line reason)_

See `roles/marketing.md` for a filled-in example of this block.

## Watch out for

PHI. Never let the model echo patient identifiers, dates of service tied to an individual, or free-text notes. Aggregate only, and suppress small cells (HIPAA Safe Harbor guidance: cells under 11 are commonly suppressed). If the file contains direct identifiers, stop and re-export de-identified.

---
Want this role promoted to a full overlay? See `CONTRIBUTING.md`.
