# Citation X-Ray Skill v1

This repository contains a reusable Agent Skill for turning legal, academic, and policy documents into audit-ready citation-level datasets.

## What it does

It helps an agent locate target-argument passages, map relevant footnotes, split independent sources, resolve ibid/supra/see-note cross-references, classify citation function, classify source type, classify source origin, list uncertain/excluded items, and optionally generate downstream statistics or visualizations.

## Local Codex layout

```text
your-project/
└── .agents/
    └── skills/
        └── citation-xray/
            ├── SKILL.md
            └── references/
```

## Example prompt

```text
Use the citation-xray skill on the uploaded PDFs.

Target argument:
[insert target argument]

Counting unit:
citation occurrence, after splitting independent sources and resolving cross-references.

Support scope:
core support + auxiliary support.

Output:
argument paragraph table, footnote table, independent source table, cross-reference table, citation function table, source classification table, and uncertain audit table. Do not generate final statistics until the uncertain table is reviewed.
```


See `skills/citation-xray/` for the skill package.
