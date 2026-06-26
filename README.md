# Citation X-Ray

[![skills.sh](https://skills.sh/b/KaiqiangZhang3/Citation_XRay)](https://skills.sh/KaiqiangZhang3/Citation_XRay)

Citation X-Ray is an Agent Skill for legal, academic, and policy citation analysis. It helps agents turn dense footnotes and references into audit-ready citation-level datasets before producing statistics, charts, or narrative conclusions.

The skill is designed for legal research, international law analysis, academic citation review, source classification, footnote auditing, and evidence-trail reconstruction.

## What It Does

Citation X-Ray guides an agent through a structured workflow:

- locate passages relevant to a target argument or research question
- map footnotes attached to those passages
- split compound footnotes into independent source items
- resolve `ibid.`, `supra`, note, paragraph, article, and internal cross-references
- classify citation function, including support, background, contrary views, duplicates, and uncertain items
- classify source type, such as scholarship, state practice, UN documents, treaties, cases, or other legal materials
- classify source origin, jurisdiction, or legal tradition
- produce an uncertain/excluded audit table before downstream statistics

## Why Use It

Citation statistics are often unreliable when an agent counts whole footnotes, treats cross-references as new sources, mistakes commentary for treaty text, or counts contrary positions as support. This skill forces the agent to build the underlying dataset first, preserve source text for audit, and make uncertainty explicit.

## Install

```bash
npx --yes skills add KaiqiangZhang3/Citation_XRay --skill citation-xray
```

To preview the available skill without installing:

```bash
npx --yes skills add KaiqiangZhang3/Citation_XRay --list --full-depth
```

## Example Prompt

```text
Use $citation-xray on the uploaded PDFs.

Target argument:
Enemy State clauses are obsolete or no longer practically applicable.

Counting unit:
Citation occurrence, after splitting independent sources and resolving cross-references.

Support scope:
Core support plus auxiliary support.

Output:
Document metadata, argument paragraph table, footnote table, independent source table, cross-reference table, citation function table, source classification table, origin table, and uncertain audit table. Do not generate final statistics until uncertain items are reviewed.
```

## Repository Structure

```text
skills/
└── citation-xray/
    ├── SKILL.md
    ├── agents/openai.yaml
    ├── examples/
    └── references/
```

`SKILL.md` contains the core trigger and workflow instructions. Detailed rules, table schemas, modular prompts, and known error patterns are stored in `references/` for progressive disclosure.

## Keywords

legal citation analysis, academic citation analysis, footnote classification, source classification, citation auditing, legal research, international law, treaty commentary, state practice, UN documents, audit-ready dataset, evidence trail, cross-reference resolution.
