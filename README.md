# Honest Data Analysis Skills

**Stop your AI from hallucinating numbers. Make every figure cite its row.**

A collection of reusable [Claude Skills](https://docs.claude.com/en/docs/claude-code/skills) that package the AI Data Analysis Playbook: a four-step workflow (Schema Check, Analyze, Visualize, Insight Brief) plus role overlays that turn any AI assistant into a careful junior analyst instead of a confident hallucinator.

Drop the `skills/` folders into `~/.claude/skills/` and the workflow is available to Claude immediately, the moment you hand it a CSV.

## Why this exists

Off-the-shelf AI prompts hallucinate. Hand a model a spreadsheet and ask "what are the trends" and it will give you a confident, well-formatted answer with invented numbers, because it was trained to produce a plausible answer, not to verify one. These skills fix that in the prompt. They give the model strict rules (only use values from the file, say "Not answerable" when stuck, cite every number), force a schema check before any analysis, demand a recomputation of every headline a second way, and make it return findings in a Claim / Evidence / Calculation / Confidence format where a guess has nowhere to hide.

This is not clever phrasing. It is an enforcement structure. You can ship deck slides off this output and defend them.

## What is in here

| Skill | What it does |
| --- | --- |
| `honest-data-analysis` | Orchestrator. Runs the full four-step workflow and pulls in a role overlay when you name your domain. |
| `data-schema-check` | Step 1, standalone. Forces the model to describe the file before it computes anything. |
| `data-analyze-honestly` | Step 2, standalone. Time patterns and category ranking, every finding cited. |
| `data-chart-specs` | Step 3, standalone. Publication-ready chart specs, not hallucinated images. |
| `data-insight-brief` | Step 4, standalone. Each chart becomes a decision-ready brief with a next step. |
| `data-cross-tool-audit` | Optional. Audit another AI's analysis against the source data. |

Nine role overlays live in `skills/honest-data-analysis/roles/` (marketing, social-video, product-analytics, saas-growth, finance-consulting, plus people-hr, ecommerce, healthcare-clinical, and education as template stubs).

## Install

Each skill is a directory with a `SKILL.md`. Claude resolves skills at `~/.claude/skills/<skill-name>/SKILL.md` (global) or `.claude/skills/<skill-name>/SKILL.md` (per-project).

### Global (available everywhere)

```bash
git clone https://github.com/TaylorONeal/data-analysis.git
cd data-analysis
# symlink every skill into your global skills dir
mkdir -p ~/.claude/skills
for d in skills/*/; do ln -s "$(pwd)/$d" ~/.claude/skills/; done
```

### Per-project (checked into one repo)

```bash
mkdir -p .claude/skills
for d in /path/to/data-analysis/skills/*/; do cp -R "$d" .claude/skills/; done
```

Prefer `cp -R` over symlinks when you want the skills committed into the project repo. Use symlinks when you want a single source of truth you can `git pull` to update.

### As a plugin marketplace (optional)

If you use Claude Code plugins, you can add this repo as a marketplace and install the bundle in one step:

```bash
/plugin marketplace add TaylorONeal/data-analysis
/plugin install honest-data-analysis@honest-data-analysis
```

See `.claude-plugin/marketplace.json` for the manifest.

## Quickstart (30 seconds)

1. Open Claude (or any AI chat) and attach a CSV. There is a sample at `examples/sample-data.csv`.
2. Invoke the schema check. In Claude Code: just say *"run a schema check on this CSV"* and the `data-schema-check` skill triggers. Or paste the prompt from `skills/data-schema-check/SKILL.md` directly.
3. The model describes the file and stops. Confirm the load looks right.
4. Say *"analyze it"* to trigger `data-analyze-honestly`. You get findings like:

```text
Claim: video delivered the lowest CPA at $11.36, 3.04x cheaper than static at $34.55.
Evidence: all 48 rows, grouped on ad_format; CPA = sum(spend) / sum(conversions).
Calculation: video = $12,799.34 / 1,127 = $11.36. static = $5,735.08 / 166 = $34.55.
Confidence: High. n=1,127 video conversions, n=166 static, full Apr 1-19 window.
```

Every number points back to rows you can open. See `examples/worked-example.md` for the full schema -> analyze -> visualize -> brief pass.

## FAQ

### What is the AI Data Analysis Playbook?

A four-step prompt framework that turns ChatGPT, Claude, or Gemini into a careful junior analyst instead of a confident hallucinator. The four prompts are Schema Check, Analyze, Visualize, and Insight Brief. You paste them in order and the model is forced to cite rows, recompute headline numbers, and refuse to answer when the data is not there.

### Why do AI models hallucinate numbers in data analysis?

Without explicit permission to refuse, models fill gaps with confident-sounding inventions. They were trained to produce a plausible answer, not to verify one. The fix is in the prompt: give the model strict rules (only use values from the file, say "Not answerable" when stuck, cite every number), force a schema check before any analysis, and demand a recomputation of headline numbers a second way.

### Which AI model is best for data analysis?

No single model wins every step. Pair them. Claude tends to be the strongest at careful reasoning, citations, and refusing when uncertain. ChatGPT is the strongest at code generation and fast iteration. Gemini integrates natively with Google Sheets. Julius.ai runs Python under the hood. Perplexity grounds answers in live web sources, useful for benchmarking your numbers against industry data. Run the same prompt through two of these and disagreements between the models will surface most hallucinations.

### How do I prevent AI hallucinations in data analysis?

Eight tactics that take ten minutes each: (1) demand citations on every number, (2) allow "I don't know" as a valid answer, (3) require a self-consistency check that recomputes the headline a second way, (4) run a schema check before any analysis, (5) cross-model audit your findings with a second AI, (6) reject vague language ("strong", "mixed", "notable"), (7) cap the date range so the model cannot extrapolate, (8) treat polished claims with no citations as the most dangerous output and verify one headline by hand before citing anywhere.

### What is the Claim, Evidence, Calculation, Confidence structure?

A four-part output format that makes hallucinations visible. Claim is one specific sentence with a number. Evidence names the source rows, column, and aggregation. Calculation shows the actual math, not adjectives. Confidence is high, medium, or low with a one-line reason. If the Calculation line is missing or vague, the claim is suspect. Send it back.

### Why ask for chart specs instead of chart images?

AI-rendered charts hallucinate axis labels and invent data points. A specification (chart type, axes, encoding, title, annotations) is a contract you can audit. You build the chart yourself in Tableau, Excel, or Looker against the actual data. A rendered PNG from an AI is a guess wearing makeup.

### How do I write a good AI prompt for analyzing a CSV file?

Three ingredients. First, strict rules at the top: only use values from the file, never invent numbers, allow "Not answerable from the data" as an answer, cite source rows on every claim. Second, a forced schema check before any analytical question. Third, a rigid output format (Claim, Evidence, Calculation, Confidence) so the model cannot bury a guess in adjectives. Copy the four prompts in this repo for a battle-tested starting point.

### How is this different from prompt engineering tutorials?

This is not about clever phrasings. It is about an enforcement structure. The four prompts work together: Schema Check makes the model prove it actually read the file, Analyze locks every finding into a citable format, Visualize asks for specifications instead of hallucinated charts, and Brief turns each finding into a decision-ready insight with a concrete next step. You can ship deck slides off this output and defend them.

### Do I need to know SQL or Python to use this?

No. The framework is for anyone uploading a CSV or pasting tabular data into a chat. If you can copy a prompt and read a number, you can use it. The model does the math. Your job is to verify the citations, recompute one headline by hand, and decide what to ship.

## Canonical reference

The polished web version of this playbook, with the prompts formatted for copy-paste, lives at **https://thinkermetrics.com/ai-data-analysis**. The prompt bodies in this repo are lifted verbatim from that page's source. Do not edit them; they are battle-tested.

## Credit

Origin: the **AI Data Analysis Playbook** by **Taylor O'Neal / [ThinkerMetrics](https://thinkermetrics.com)**. Packaged as Claude Skills here for anyone who wants the workflow in their own environment.

## License

MIT. See `LICENSE`.
