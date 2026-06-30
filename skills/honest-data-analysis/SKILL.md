---
name: honest-data-analysis
description: Use when the user wants to analyze a CSV or tabular dataset with an AI assistant and needs the analysis to be defensible, cited, and free of hallucinated numbers; runs the full four-step Schema, Analyze, Visualize, Brief workflow and applies a role overlay when the user names their domain (marketing, social, product, saas, finance, and more).
---

# Honest data analysis

A four-step workflow that turns a general AI assistant into a careful junior analyst instead of a confident hallucinator. Use it whenever someone hands you a CSV and says "analyze this," "find patterns in this," or "what does this data say."

The model is forced to cite rows, recompute headline numbers a second way, and refuse when the data is not there.

## Run the steps in order

Each step is a prompt you paste into the same chat, with the CSV attached. Full prompt text lives in `references/`:

1. **Schema check** - `references/01-schema-check.md`. Make the model describe the file and stop. No analysis yet.
2. **Analyze** - `references/02-analyze.md`. Time patterns plus category ranking, every finding as Claim / Evidence / Calculation / Confidence.
3. **Visualize** - `references/03-visualize.md`. Chart specifications, not rendered images.
4. **Insight brief** - `references/04-insight-brief.md`. Each chart becomes a decision-ready brief with one concrete next step.

Optional fifth step when you want a second opinion: `references/cross-tool-audit.md` runs a finding through a second AI and labels each claim VERIFIED, DISAGREES, or UNCHECKABLE.

## Apply a role overlay

If the user names their domain, load the matching file in `roles/` and plug its data sources, primary metric, grouping column, and time grain into the Analyze prompt. Available overlays:

- `roles/marketing.md` - Meta Ads, email, paid social
- `roles/social-video.md` - YouTube, TikTok, short-form
- `roles/product-analytics.md` - Mixpanel, Amplitude, Heap
- `roles/saas-growth.md` - Stripe, HubSpot, billing
- `roles/finance-consulting.md` - P&Ls, segment revenue
- `roles/people-hr.md`, `roles/ecommerce.md`, `roles/healthcare-clinical.md`, `roles/education.md` - template stubs (structure and the domain gotcha; fill the numbers with your own data)

## Supporting references

- `references/anti-hallucination-tactics.md` - the 8 tactics and the 5-tool pairing matrix
- `references/pre-ship-checklist.md` - run before you cite anything anywhere
- `references/glossary.md` - key terms

## The non-negotiables

Demand citations on every number. Allow "I don't know." Make the model recompute the headline a second way. Reject vague language. Cap the date range so it cannot extrapolate. A polished claim with no citation is the most dangerous output; verify one headline by hand.

See `examples/worked-example.md` for a full pass against `examples/sample-data.csv`.

Origin: the AI Data Analysis Playbook by Taylor O'Neal / ThinkerMetrics. Canonical web reference: https://thinkermetrics.com/ai-data-analysis
