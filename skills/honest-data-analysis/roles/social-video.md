# Social Media Manager
*YouTube Studio, TikTok Creator, short-form video*

## Plug into the prompt

- **Data sources:** YouTube Studio CSV, TikTok Creator analytics, TubeBuddy exports
- **Primary metric column:** Avg view duration, retention %, thumbnail CTR, shares, follower delta.
- **Grouping column:** Video format (Short, long-form, tutorial, reaction), thumbnail style, hook type.
- **Time grain:** Per-video. Weekly rollup for trend.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** TikToks with a hook under 3 seconds held 67% retention vs 41% for slower openers, last 30 days.
- **Evidence:** Rows 4 to 89, hook_seconds (computed from caption start), retention_pct column.
- **Calculation:** Mean retention for hook < 3s (n=42) = 0.674. Mean for hook >= 3s (n=44) = 0.412.
- **Confidence:** High. n=86 videos across 30 days, same posting cadence.

## Watch out for

Viral outliers. Have the model report median alongside mean and flag posts > 3 SDs from the mean.

---
Lifted verbatim from the ROLES data in the AI Data Analysis Playbook: https://thinkermetrics.com/ai-data-analysis
