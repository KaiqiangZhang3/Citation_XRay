# Publishing Guide for skills.sh / Open Agent Skills

## What this package is

This is a publish-ready skill directory. It contains a SKILL.md file with YAML frontmatter and supporting reference files.

## What an AI chat session cannot do

This chat cannot directly publish to your skills.sh account or GitHub account without your credentials and repository access.

## Minimal GitHub workflow

1. Create a new GitHub repository, for example citation-xray-skill.
2. Put the skill directory in the repo.

Suggested structure:

```text
citation-xray-skill/
└── skills/
    └── citation-xray/
        ├── SKILL.md
        ├── references/
        ├── examples/
        └── agents/
```

3. Commit and push.
4. Test installation with the Skills CLI:

```bash
npx skills add <your-github-username>/citation-xray-skill
```

## Local Codex test

Copy the skill directory to:

```text
your-repo/.agents/skills/citation-xray/
```

Then launch Codex in that repo. If the skill does not appear, restart Codex.
