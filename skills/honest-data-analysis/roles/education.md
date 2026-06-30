# Education or Institutional Research Analyst
*LMS exports, SIS records, enrollment and outcomes data*

> **Template stub.** This role is not yet in the canonical `data.ts` ROLES data, so the "what good output looks like" numbers below are intentionally left blank. The structure and the domain gotcha are real. Fill the Claim / Evidence / Calculation / Confidence with figures computed from your own file. Do not invent them; that is the one thing this whole repo exists to prevent.

## Plug into the prompt

- **Data sources:** LMS gradebook export (Canvas, Blackboard), SIS enrollment CSV, course evaluations.
- **Primary metric column:** Pass rate, DFW rate, retention, completion %, average grade, enrollment delta.
- **Grouping column:** Course, section, instructor, term, student cohort or major.
- **Time grain:** Per-term, with year-over-year comparisons.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** _(one specific sentence with a number, computed from your data)_
- **Evidence:** _(source rows, column, aggregation)_
- **Calculation:** _(the actual math)_
- **Confidence:** _(high / medium / low, with sample size and a one-line reason)_

See `roles/marketing.md` for a filled-in example of this block.

## Watch out for

FERPA. Student-level records are protected education records. Report cohort aggregates, suppress any subgroup under the institution reporting threshold (often n < 10), and never let the model surface a named student row or an identifiable grade.

---
Want this role promoted to a full overlay? See `CONTRIBUTING.md`.
