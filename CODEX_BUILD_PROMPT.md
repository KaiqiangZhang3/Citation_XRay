# Codex Build Prompt

You are helping me turn the included Citation X-Ray specification into a publishable Agent Skill for the open agent skills ecosystem.

Goal: Create a clean, publish-ready skill repository that can be installed with the Skills CLI and used by Codex, Cursor, Claude Code, and other agents that support SKILL.md-style skills.

Requirements:

1. Preserve the workflow: locate target-argument passages; map footnotes; split independent sources; resolve ibid/supra/see-note/MN/article cross-references; classify citation function; classify source type; classify origin/jurisdiction; list uncertain/excluded items; generate optional downstream outputs only after audit review.
2. Keep SKILL.md concise enough for progressive disclosure. Move detailed rules to references/*.md.
3. Ensure SKILL.md has valid YAML frontmatter with name and description.
4. Do not turn this into a statistics-only skill. It is a backend data-foundation skill.
5. Validate that internal cross-references are not counted as new sources, contrary views are not counted as support, scholarly works about treaties are not classified as treaties, and uncertain classifications are not guessed.
6. Produce final file tree, install/test commands, quality checklist, and unresolved human decisions.
