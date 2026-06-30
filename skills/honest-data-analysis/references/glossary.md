# Glossary

**Schema check**

A forced inspection of the uploaded file before any analytical question. The model lists columns, types, row count, date range, and missing values. If it cannot describe the file, every number it gives next is a guess.

**Grounding**

Restricting model output to values that appear in the source data. The prompt rule is: "Use ONLY values that appear in the uploaded file. Never invent rows, dates, names, or numbers."

**Self-consistency check**

Recomputing a headline number a second way (different aggregation, different formula) and comparing. Disagreement between the two methods is a flag, not a tiebreaker.

**Cross-tool audit**

Running the same finding through a second AI model. Disagreements between models surface hallucinations faster than any single tool. Label each claim VERIFIED, DISAGREES, or UNCHECKABLE.

**Claim, Evidence, Calculation, Confidence**

The four-part output structure that every finding must follow. Claim is one specific sentence. Evidence cites source rows and column. Calculation is the actual math. Confidence is high, medium, or low with a one-line reason.

**Chart spec**

A written specification (chart type, axes, encoding, title, annotations) you build into a real chart yourself, instead of asking the AI to render an image. Specs can be audited. Rendered images cannot.

**Insight brief**

A four-part summary for each chart: The Insight (one specific sentence), Why It Matters (tied to a business goal), Data Connection (citing rows and sample size), Next Steps (one concrete action). Decision-ready.

**Hallucination**

A confident model output that has no basis in the source data. Often appears as a plausible number, a non-existent row, or an extrapolation past the date range. The four-step framework is designed to make hallucinations visible.
