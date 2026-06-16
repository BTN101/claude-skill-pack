# claude-skill-pack

A curated collection of Claude skills organized into domain layers — covering engineering, product thinking, founder/GTM work, design quality, and document creation.

Built for use with [Claude's skill system](https://docs.claude.ai) on claude.ai.

---

## What are Claude Skills?

Skills are structured instruction sets that tell Claude *how* to approach a specific task — what workflow to follow, what quality gates to apply, what patterns to enforce. They're loaded into context when a matching task comes up, giving Claude specialist-level discipline rather than generic help.

Each skill lives in a folder with a `SKILL.md` file. The frontmatter `description` field is what triggers the skill — Claude reads it and decides whether to apply the skill based on your request.

```
skill-name/
├── SKILL.md          # Required: name, description, instructions
└── references/       # Optional: supporting docs loaded on demand
```

---

## Skill Layers

This pack introduces **layer skills** — meta-skills that group related specialists together. Instead of needing to know which exact skill to reach for, you describe the task and the layer routes to the right one automatically.

| Layer | Domain | Skills Inside |
|---|---|---|
| `founder-layer` | Business, investors, GTM, content | investor-materials, investor-outreach, market-research, brand-voice, copywriting, article-writing, launch-strategy, pricing-strategy, competitive-landscape |
| `engineering-layer` | Code, architecture, APIs, security | api-design, backend-patterns, security-review, react-patterns, react-performance, nextjs-app-router-patterns, postgres-patterns, database-migrations, deployment-patterns, tdd-workflow, java-coding-standards |
| `security-layer` | Security auditing, vulnerability hunting, vibe-coded app hardening | security-review, find-bugs, gha-security-review, code-review |
| `product-layer` | Product strategy, discovery, specs | product-lens, lean-startup, 37signals-way, mom-test, jobs-to-be-done, prioritization-advisor, prd-development, hooked-ux, user-story |
| `design-layer` | UI quality, motion, anti-slop | impeccable, design-taste-frontend, redesign-existing-projects, framer-motion-animator, animation-micro-interaction-pack |
| `document-layer` | File creation and reading | docx, pptx, xlsx, pdf, file-reading, pdf-reading |

---

## How It Works

```
You:    "Cold email an investor about my fraud detection startup"
         ↓
Layer:  founder-layer triggers on "investor" + "email"
         ↓
Skill:  investor-outreach runs its structured workflow
         ↓
Output: A tight, personalized, proof-first email — not generic copy
```

The layer skill is the router. The individual skills are the knowledge. Both need to be installed.

---

## Skills in This Pack

### 🟠 Layers (`skills/layers/`)

| Skill | What it does |
|---|---|
| `founder-layer` | Routes business, investor, GTM, and content tasks |
| `engineering-layer` | Routes code, architecture, security, and deployment tasks |
| `security-layer` | Routes security audits, vulnerability hunts, and vibe-coded app hardening |
| `product-layer` | Routes product strategy, discovery, and spec tasks |
| `design-layer` | Routes UI quality, motion, and design audit tasks |
| `document-layer` | Routes file creation and reading tasks |

### ⚙️ Engineering (`skills/engineering/`)

| Skill | What it does |
|---|---|
| `security-review` | Secrets management, input validation, SQL injection, XSS, CSRF, auth, RLS |
| `find-bugs` | Branch-diff scanner — maps attack surface, runs OWASP checklist per changed file |
| `gha-security-review` | GitHub Actions audit — pwn-request, expression injection, supply chain, credential theft |
| `code-review` | Holistic PR review — runtime errors, N+1s, perf, backwards compat, security |
| `api-design` | REST naming, status codes, pagination, versioning, error format |
| `backend-patterns` | Repository + service layer, caching, background jobs, middleware |
| `react-patterns` | Composition, compound components, custom hooks, context |
| `react-performance` | Memoization, code splitting, Server Components, waterfall fixes |
| `react-testing` | Testing Library, Vitest/Jest, MSW mocking, accessibility assertions |
| `postgres-patterns` | Query optimization, indexing, connection pooling, RLS |
| `database-migrations` | Safe schema changes, rollbacks, zero-downtime migrations |
| `deployment-patterns` | Vercel, Docker, CI/CD, health checks, rollback strategy |
| `tdd-workflow` | Test-driven development, 80%+ coverage target |
| `java-coding-standards` | Spring Boot / Quarkus naming, immutability, streams, exceptions |

### 🧠 Founder (`skills/founder/`)

| Skill | What it does |
|---|---|
| `investor-materials` | Pitch decks, one-pagers, financial models, accelerator applications |
| `investor-outreach` | Cold emails, warm intros, follow-ups — proof over adjectives |
| `market-research` | TAM/SAM/SOM sizing, competitive analysis, investor diligence |
| `brand-voice` | Reusable voice profile from real source material |
| `article-writing` | Blog posts, articles, technical essays, newsletters |

### 🔭 Product (`skills/product/`)

| Skill | What it does |
|---|---|
| `product-lens` | Founder diagnostic — who is this for, what's the pain, what's the MVP |

---

## Installation

### Install a `.skill` file on claude.ai

1. Download the `.skill` file from the [releases page](../../releases)
2. Go to [claude.ai](https://claude.ai) → Settings → Skills
3. Click **Install skill** and select the `.skill` file
4. The skill is now active across your conversations

### Install from source

Clone the repo and use any `SKILL.md` directly — the file format is plain markdown with YAML frontmatter.

```bash
git clone https://github.com/BTN101/claude-skill-pack
```

---

## Skill File Format

Every skill follows this structure:

```markdown
---
name: skill-name
description: When to trigger and what the skill does. This is the
             primary mechanism — Claude matches your request against
             all skill descriptions to decide what to load.
---

# Skill Name

Instructions for Claude go here in plain markdown.

## When to Activate
## Workflow
## Quality Gate
```

The `description` field is the most important part. It acts as the trigger — so it needs to be specific about both *what* the skill does and *when* it should fire.

---

## Contributing

Skills are just markdown files. To add one:

1. Create a folder under the relevant category in `skills/`
2. Add a `SKILL.md` with proper YAML frontmatter
3. Optionally add a `references/` folder for supporting docs
4. Submit a PR

Good skills have: a precise trigger description, a clear workflow, and a quality gate before output.

---

## Why This Exists

Most AI assistance is generic. Skills make it structural — the same way a senior engineer follows a checklist before shipping an API endpoint, or a founder applies a framework before deciding what to build. This pack is an attempt to encode that discipline into reusable, shareable form.

---

## License

MIT — use freely, modify as needed, attribution appreciated.

---

*Built by [@BTN101](https://github.com/BTN101) · Centurion, South Africa*
