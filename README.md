# Claude Code Skills

Reusable [Claude Code skills](https://docs.anthropic.com/en/docs/claude-code/skills) for project scaffolding and development.

## Directory Structure

```
claude-skills/
├── README.md
└── skills/
    ├── nextjs16-setup/
    │   └── SKILL.md
    └── <future-skill>/
        └── SKILL.md
```

## Available Skills

| Skill | Description | ~Tokens |
|-------|-------------|---------|
| `nextjs16-setup` | Next.js 16 project conventions, setup, and best practices | ~10K |

## How to Add a Skill to Your Project

Claude Code loads skills from your project's `.claude/skills/` directory. Copy the skill folder you need into that directory.

### Quick Setup

From your project root:

```bash
# 1. Create the skills directory (if it doesn't exist)
mkdir -p .claude/skills

# 2. Copy the skill you need
cp -r ~/projects/claude-skills/skills/nextjs16-setup .claude/skills/
```

Your project should end up like:

```
my-project/
├── .claude/
│   └── skills/
│       └── nextjs16-setup/
│           └── SKILL.md
├── src/
├── package.json
└── ...
```

### Multiple Skills

Copy as many skills as your project needs:

```bash
mkdir -p .claude/skills
cp -r ~/projects/claude-skills/skills/nextjs16-setup .claude/skills/
cp -r ~/projects/claude-skills/skills/wordpress-theme .claude/skills/
```

### Git

Commit the `.claude/` directory so skills are available to all collaborators:

```bash
git add .claude/skills/
git commit -m "chore(claude): add project skills"
```

## How Skills Work

- Claude Code automatically loads a skill's `SKILL.md` when your prompt matches the **trigger keywords** in the skill's frontmatter `description` field
- Skills are loaded **once per conversation**, not per message
- Only the `SKILL.md` file is loaded — other files in the skill directory are not auto-loaded
- Each skill consumes context tokens (shown in the table above) out of Claude's 200K context window

## Creating a New Skill

1. Create a new folder under `skills/`:

```bash
mkdir -p skills/my-new-skill
```

2. Add a `SKILL.md` with YAML frontmatter:

```yaml
---
name: my-new-skill
description: >
  What this skill does. Include trigger keywords that should
  activate this skill (e.g., "wordpress", "custom theme",
  "theme development").
---

# My New Skill

Content goes here...
```

3. Update the **Available Skills** table in this README

### Frontmatter Tips

- `name` — kebab-case, matches the folder name
- `description` — include all keywords/phrases that should trigger this skill. Claude Code matches your prompt against this field to decide whether to load the skill.

### Sizing Guidelines

- Aim for **under 15K tokens** per skill (~1,000 lines) to leave room for conversation context
- If a skill exceeds that, consider whether all sections are needed during coding or if some are reference-only
- One focused skill is better than one giant catch-all

## Updating a Skill

When you update a skill in this repo, re-copy it to each project that uses it:

```bash
# From your project root
cp -r ~/projects/claude-skills/skills/nextjs16-setup .claude/skills/
```

## Removing a Skill from a Project

```bash
# From your project root
rm -rf .claude/skills/nextjs16-setup
```
