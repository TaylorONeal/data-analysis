# Contributing

This repo packages a battle-tested workflow. Contributions are welcome, but the bar is specific: nothing here should make the output easier to fake.

## Two things you might add

### 1. A new role overlay

Roles live in `skills/honest-data-analysis/roles/<role>.md`. Four of them (people-hr, ecommerce, healthcare-clinical, education) are template stubs waiting for real numbers. To promote a stub or add a new role, the file needs:

- **Heading:** role name and a one-line subtitle.
- **Plug into the prompt:** data sources, primary metric column, grouping column, time grain.
- **What good output looks like:** a Claim / Evidence / Calculation / Confidence block with *real numbers computed from a real (or realistic, clearly-labeled) file*. Do not invent figures and present them as observed. If you do not have data, leave the stub markers in place.
- **Watch out for:** the one domain-specific gotcha (attribution windows, PHI, FERPA, gross-vs-net, small-n re-identification).

Copy `roles/marketing.md` as the model for a filled-in overlay.

### 2. An improvement to a prompt

The five prompts (`SCHEMA`, `ANALYZE`, `VISUALIZE`, `BRIEF`, `AUDIT`) are the source of truth and are mirrored verbatim from `data.ts` in the ThinkerMetrics site. **Do not edit a prompt body in isolation here.** If you have a real improvement:

1. Open an issue describing the change and why, with a before/after example on a real dataset.
2. The canonical edit happens upstream in the playbook source, then flows back into the reference and skill files so the two stay identical.

This keeps the repo and the live page from drifting apart.

## Skill file rules

Every `SKILL.md` must:

- have YAML frontmatter with a kebab-case `name` and a one-sentence `description` (under 1024 characters) that says *when* to use it;
- keep the body concise and push long content into `references/` (progressive disclosure);
- avoid dangling links (every `references/...` or `roles/...` path must resolve).

## Voice

Direct, peer-to-peer, lightly opinionated. No "in today's data-driven world." No em dashes. Match the existing files.
