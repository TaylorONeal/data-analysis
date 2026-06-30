# Anti-hallucination tactics

Eight tactics that take about ten minutes each. They are the spine of every prompt in this repo.

**01. Demand citations.** Every number must come with source rows and the formula. No cite, no trust.

**02. Allow "I don't know."** Give the model permission to refuse. Without it, models invent.

**03. Self-consistency check.** Have the model recompute the headline a second way. Disagreement is a flag.

**04. Schema first.** Make the model describe the file before asking analytical questions.

**05. Cross-model audit.** Run the same finding through a second AI. Disagreements between models are signal.

**06. Reject vague language.** "Performance was mixed" gets sent back. Demand a number or a deletion.

**07. Cap the date range.** Add "do not extrapolate beyond the data" to every prompt. Every time.

**08. Beware confident wrongness.** A polished claim with no citations is the most dangerous output. Verify one headline by hand.

## Which tool for which step

No single model wins every step. Pair them. Run the same prompt through two and let the disagreements surface the hallucinations.

| Tool | Role | Best for | Notes |
| --- | --- | --- | --- |
| Claude | careful reasoner | Schema, Analyze | Best at careful reasoning, citations, and refusing when uncertain. Use for schema checks and analysis where admitting "I don't know" matters. |
| ChatGPT | code generator | Code, Pivots | Best at code generation and fast iteration. Use for generated Python or R, pivot-table breakdowns, ad-hoc transforms. |
| Gemini | sheets-native | Sheets, Quick | Free, integrates with Google Sheets. Use when the data already lives in Sheets and you don't want to export. |
| Julius.ai | python notebook | Explore, Plots | Runs Python under the hood and returns plots inline. Use for quick exploratory charts when you want to look, not export. |
| Perplexity | web grounding | Benchmarks, Sources | Live web search with sources. Use to benchmark your numbers against industry data, not to analyze the file itself. |
