# Contributing

Skills are plain markdown — no build step, no dependencies.

## Adding a skill

1. Pick the right category folder under `skills/`
2. Create `skills/<category>/<skill-name>/SKILL.md`
3. Use this frontmatter at the top:

```markdown
---
name: your-skill-name
description: A specific description of when this skill should trigger
             and what it does. This is the primary matching mechanism —
             be precise about both the task type and the context.
---
```

4. Write the skill body in plain markdown
5. Add a `references/` subfolder if you have supporting docs
6. Submit a PR with a one-line description of what the skill does

## What makes a good skill

- **Precise trigger description** — Claude matches your request against the description to decide whether to load it. Vague descriptions cause misfires.
- **Clear workflow** — steps in order, not a list of principles
- **Quality gate** — explicit checks before delivering output
- **Under 500 lines** — if longer, use a `references/` folder for supporting material

## Skill categories

| Folder | For |
|---|---|
| `skills/layers/` | Meta-skills that route to other skills |
| `skills/engineering/` | Code, architecture, security, testing, deployment |
| `skills/founder/` | Business, investors, GTM, content |
| `skills/product/` | Product strategy, discovery, prioritization, specs |
| `skills/design/` | UI quality, motion, design auditing |
| `skills/documents/` | File creation and reading |
