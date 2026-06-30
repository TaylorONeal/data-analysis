---
name: data-cross-tool-audit
description: Use when auditing analysis produced by another AI tool against the source data, labeling every claim VERIFIED, DISAGREES, or UNCHECKABLE.
---

# Cross-tool audit

Run a finding from one AI through a second one. Disagreements between models surface hallucinations faster than any single tool. Every claim gets labeled VERIFIED, DISAGREES, or UNCHECKABLE.

Paste this prompt into your AI tool (Claude, ChatGPT, Gemini) with the CSV attached:

```text
I just ran the analysis below in another AI tool. Audit it against the same data file (which I am uploading here).

STRICT RULES:
1. Use ONLY values from the data file. Never trust the other tool's numbers without verification.
2. For every claim, label it:
  - VERIFIED: I recomputed and got the same number. Show your calculation.
  - DISAGREES: I recomputed and got a different number. Show both.
  - UNCHECKABLE: The claim is too vague to verify, or the data isn't in the file.

TASK:
A. Audit each numerical claim using the labels above.
B. List any claim the other tool made that you would not make from this data, and why.
C. List any insight in the data that the other tool missed.
D. Final verdict: which findings are reliable, which need more data, which to discard.

Pasted output from the other tool:
"""
[PASTE THE FIRST TOOL'S OUTPUT HERE]
"""

Be blunt. If the other tool hallucinated, call it out by row.
```

Paste the first tool's output where the prompt marks it and attach the same data file. Be ready for it to be blunt.

Source: this prompt is lifted verbatim from the AI Data Analysis Playbook at https://thinkermetrics.com/ai-data-analysis. Do not edit the prompt body; it is battle-tested.
