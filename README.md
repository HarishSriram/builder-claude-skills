# Builder Claude Skills

Reusable [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills for software engineering workflows.

## Available Skills

| Skill | Description |
|-------|-------------|
| [audit-docs](skills/audit-docs/SKILL.md) | Audits all markdown files in a repository for repetition, stale content, factual inconsistencies, organisational issues, and token efficiency. |

## Installation

### Quick install (all skills)

```bash
git clone https://github.com/HarishSriram/builder-claude-skills.git
cd builder-claude-skills
bash install.sh
```

### Install a single skill

```bash
git clone https://github.com/HarishSriram/builder-claude-skills.git
mkdir -p ~/.claude/skills/audit-docs
cp builder-claude-skills/skills/audit-docs/SKILL.md ~/.claude/skills/audit-docs/SKILL.md
```

### Update to latest

```bash
cd builder-claude-skills
git pull
bash install.sh
```

## Usage

Once installed, skills are available in any Claude Code session. Invoke them with `/skill-name`:

```
/audit-docs
```

## Adding to a project (team use)

To make a skill available to everyone working on a specific repo, copy it into the project's `.claude/skills/` directory instead:

```bash
mkdir -p .claude/skills/audit-docs
cp builder-claude-skills/skills/audit-docs/SKILL.md .claude/skills/audit-docs/SKILL.md
git add .claude/skills/
git commit -m "Add audit-docs skill"
```

## Contributing

Issues and PRs welcome. Each skill lives in `skills/<name>/SKILL.md` following the [Claude Code skill format](https://docs.anthropic.com/en/docs/claude-code).
