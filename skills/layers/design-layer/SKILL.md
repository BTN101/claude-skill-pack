---
name: design-layer
description: Activate this skill group for any UI, UX, visual design, or interface quality task. Triggers include: the UI looks generic, this looks like AI slop, redesign this, audit this interface, add animations, add micro-interactions, make this feel more polished, Framer Motion, motion design, design review, critique this layout, improve the visual hierarchy, it feels flat, the onboarding is bad, empty state, loading state looks ugly, make it feel premium, and any request where the goal is improving how something looks or feels rather than how it works. Also triggers when Seb shares a screenshot and asks for feedback on the visual design.
---

# Design Layer

This group covers UI quality, motion design, and interface auditing. When activated, identify which sub-skill applies and follow its workflow.

## Skill Map

### Quality Auditing (Start Here for Any Design Review)
- **impeccable** — the AI slop detector. Audits UI against professional design standards: visual hierarchy, typography, spacing, cognitive load, accessibility, responsive behavior. Scores the interface and lists specific problems. **Run this first whenever reviewing or critiquing any UI.**
- **design-taste-frontend** — senior UI/UX engineer mode. Enforces metric-based rules, bans AI default aesthetics (generic purple gradients, card-heavy layouts), applies Framer Motion patterns, performance guardrails, and full interaction states at the code level.
- **redesign-existing-projects** — upgrades existing codebases to premium quality. Audits current code, identifies generic AI patterns, applies targeted fixes without rewriting from scratch.

### Motion & Interaction
- **framer-motion-animator** — page transitions, gesture feedback, entrance animations, orchestrated sequences using Framer Motion. Use when adding any animation to a React project.
- **animation-micro-interaction-pack** — hover effects, button feedback, loading indicators, skeleton states, reduced-motion support. Use when adding micro-interactions or polishing the feel of a UI.

## How to Use

1. For a design review or critique: start with **impeccable**, which will score the interface and surface the top issues.
2. For building new components with high design quality: use **design-taste-frontend** to set the coding standards before writing any JSX.
3. For upgrading existing code that looks generic: use **redesign-existing-projects**.
4. For adding motion: **framer-motion-animator** for page/route transitions and complex sequences; **animation-micro-interaction-pack** for component-level polish.

## What "Good" Looks Like

- No generic AI purple gradients or excessive card grids.
- Typography has clear hierarchy (not everything the same size and weight).
- Interactive elements have hover, active, focus, and disabled states.
- Loading states are skeletons, not spinners where possible.
- Empty states have a clear action, not just "No data found."
- Animations are purposeful — they communicate state change, not just decorate.
- Mobile-first, reduced-motion respected.
