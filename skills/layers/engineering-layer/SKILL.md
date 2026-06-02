---
name: engineering-layer
description: Activate this skill group for any technical, coding, or architecture task. Triggers include: building an API, designing endpoints, backend architecture, database schema, SQL queries, Postgres, migrations, React component, Next.js, Zustand state, Tailwind, shadcn, authentication, security checklist, JWT, input validation, secrets, deployment, Vercel, CI/CD, Docker, Java code, test-driven development, unit tests, React testing, performance optimization, memoization, code splitting, and any request where the primary deliverable is working code or a technical architecture decision. Use this skill group whenever Seb is building, debugging, or architecting anything for Antibody, SchoolOrder, or his GitHub portfolio.
---

# Engineering Layer

This group covers the full technical stack: API design, backend, frontend, database, security, testing, deployment, and Java. When activated, identify the relevant sub-skill and follow its workflow.

## Skill Map

### Security (Read First for Any Backend Work)
- **security-review** — comprehensive security checklist: secrets management, input validation, SQL injection, XSS, CSRF, auth/JWT, rate limiting, RLS. **Read this before shipping any API endpoint, auth flow, or form that handles user data.** Antibody especially.

### API & Backend
- **api-design** — REST resource naming, HTTP status codes, pagination (cursor vs offset), filtering, versioning, error response format. Use when designing any API endpoint.
- **backend-patterns** — repository pattern, service layer, N+1 fixes, Redis caching, background jobs, middleware. Use when architecting the backend or adding a new service layer.

### Frontend & React
- **react-patterns** — composition, compound components, custom hooks, render props, context patterns. Use when building React components.
- **react-performance** — memoization, virtualization, bundle splitting, Server Components, waterfall elimination. Use when a component is slow or a page feels heavy.
- **nextjs-app-router-patterns** — App Router, Server Components, streaming, parallel routes, data fetching. Use when working in Next.js 14+.
- **zustand-state-builder** — Zustand store setup, persistence, devtools, modular slices. Use when setting up or extending global state.
- **state-ux-flow-builder** — loading/error/empty/success states, state machines for complex UI flows. Use when a component has multiple data-fetching states.
- **shadcn-ui** — shadcn/ui component integration, customization, theming. Use when adding or modifying shadcn components.
- **tailwind-design-system** — Tailwind v4, design tokens, component libraries, responsive patterns. Use when building a design system or standardizing UI.

### Database
- **postgres-patterns** — query optimization, indexing, connection pooling, Supabase RLS. Use when writing or reviewing Postgres queries.
- **database-migrations** — safe schema changes, rollbacks, zero-downtime migrations across Prisma/Drizzle/raw SQL. Use before running any DB migration in production.

### Testing
- **tdd-workflow** — test-driven development with 80%+ coverage: unit, integration, E2E. Use when writing new features or fixing bugs the proper way.
- **react-testing** — React Testing Library, Vitest/Jest, MSW for mocking, accessibility assertions. Use when writing component tests.

### Deployment & Infrastructure
- **deployment-patterns** — Vercel, Railway, Docker, CI/CD pipelines, health checks, rollback strategy. Use when deploying or setting up a new deployment pipeline.

### Java (School/Portfolio)
- **java-coding-standards** — Spring Boot / Quarkus naming, immutability, Optional, streams, exceptions, generics. Use when writing Java for school assignments or the GitHub portfolio projects.

### Prompting & AI
- **prompt-template-builder** — reusable prompt templates with strict output contracts, few-shot examples, format rules. Use when building prompts for Antibody's AI detection layer.

## How to Use

1. Identify the right sub-skill from the map above.
2. Read its SKILL.md at `/mnt/skills/user/<skill-name>/SKILL.md`.
3. **Always read security-review before touching any endpoint that handles user data, API keys, or authentication.**
4. For new features: read api-design → backend-patterns → security-review in that order.
5. For new React work: react-patterns first, then react-performance if performance is a concern.

## Non-Negotiables

- No hardcoded secrets ever.
- All user inputs validated with a schema (Zod on the frontend, equivalent on backend).
- RLS enabled on all Supabase tables.
- Every API endpoint follows the status code reference in api-design.
