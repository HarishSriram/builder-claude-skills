# Builder Claude Skills

A collection of [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills I've built or found useful while building products. Topics range from documentation hygiene to design systems to whatever else turns out to be worth automating.

## Installation

```
/plugin marketplace add HarishSriram/builder-claude-skills
/plugin install builder-skills@builder-claude-skills
```

## Skills

| Skill | Invocation | What it does |
|-------|------------|--------------|
| Repo Docs Audit | `/builder-skills:audit-docs` | 7-step audit of all markdown files in a repo — catches repetition, stale content, factual inconsistencies, organisational issues, and token inefficiency. Reports only; waits for approval before changing anything. |

## Contributing

Issues and PRs welcome. Skills live in `plugins/builder-skills/skills/<name>/SKILL.md`.
