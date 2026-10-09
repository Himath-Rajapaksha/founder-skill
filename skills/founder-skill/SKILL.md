---
name: founder-skill
description: Use when starting a new web app or project from scratch, before writing any application code (scaffolding, package.json, schema, components). Also use when about to skip planning under time pressure, when the user asks to skip planning docs, or when tempted to retrofit specs from already-written code.
---

# Founder Skill — Web Project Specification Package

## Overview

**No application code until the six-document Specification Package exists and is approved.** Specs are the fast path, not overhead: every assumption you skip is rework you pay later. Violating the letter of the gate is violating its spirit.

## The Hard Gate

Refuse to create application code until `docs/specs/` contains all six documents below and the user has approved them (explicit yes, or "looks good, build it").

**Application code means:** scaffolding, `package.json`, server files, schema DDL, components, routes, seed scripts. **Allowed before approval:** writing/updating the six docs, environment probes (`node -v`, `pg_isready`), reading existing files.

**Canonical Six — always exactly these, never substitutes:** Product Requirements Document (PRD), Technical Specification, User Flow Document, Design System Guidelines, Data Model & Access Control Document, Project Delivery Plan. Do not invent your own equivalent set (no "API contract instead of Technical Specification", no "roles doc instead of Data Model & Access Control"). If a doc feels redundant for a simple app, write it shorter — do not replace it.

## The Specification Package

| # | Document | File | Answers |
|---|----------|------|---------|
| 1 | Product Requirements Document (PRD) | `docs/specs/01-prd.md` | Functional scope, feature-level behaviors, business objectives |
| 2 | Technical Specification | `docs/specs/02-technical-spec.md` | Infrastructure stack (e.g. React, Node.js, PostgreSQL), architectural decisions |
| 3 | User Flow Document | `docs/specs/03-user-flow.md` | Primary user journeys, interaction triggers, page transitions |
| 4 | Design System Guidelines | `docs/specs/04-design-system.md` | Color palette, typography, UI component parameters |
| 5 | Data Model & Access Control Document | `docs/specs/05-data-model-rbac.md` | Relational data models, RBAC matrix, storage configuration |
| 6 | Project Delivery Plan | `docs/specs/06-project-plan.md` | Phased timeline, build sequence, post-launch monitoring |

Create them in order — each feeds the next.

## Workflow (Hybrid)

1. **Collect the brief.** If the user gave a description, use it. If missing essentials (what the app does, who uses it), ask focused questions — one round, not an interrogation.
2. **Draft all six** under `docs/specs/` with sensible defaults, marking uncertain choices `> DECISION NEEDED: ...`.
3. **Interview to fill gaps.** Walk the user through only the `DECISION NEEDED` items. Revise docs with their answers.
4. **Approval gate.** Present a one-paragraph summary per doc and ask for approval of all six. Do not start coding in the same turn you present them.
5. **Build.** Only after approval, implement per `06-project-plan.md`.

## Red Flags — STOP

- Reaching for `npm create`, writing `package.json`, or `schema.sql` before all six docs are approved
- "I'll just scaffold quickly while we figure out the docs"
- "This is simple CRUD — docs are overkill"
- User says "skip the docs" and you comply without first presenting the gate once
- Writing docs that describe code you already wrote, instead of design decisions made before code
- Retroactive docs offered as a substitute ("I'll reverse-engineer the data model doc from what I built")
- Inventing a different set of six documents, or swapping one canonical doc for an "equivalent"

## Rationalization Table

| Excuse | Reality |
|--------|---------|
| "Demo/deadline in N days — defaults are correct" | Drafting the package from a brief takes under 30 minutes. A wrong default discovered mid-build costs days. Docs ARE the fast path. |
| "User explicitly said no planning docs" | Present the gate once with the tradeoff, then immediately draft all six so review is one pass. Respecting the user means not wasting their build on the wrong features. |
| "Simple CRUD doesn't need this" | Simple apps have the most undocumented assumptions (auth? roles? statuses?). Docs catch them in minutes. |
| "I'll write the docs after the code" | Reverse-engineered docs describe what was built, not what should be built. They cannot gate decisions already made. |
| "I already scaffolded — too late" | Sunk cost. Stop, write the six docs against what exists, then continue. Code written without specs is code you may delete. |
| "Asking questions in chat achieves the same" | Chat answers evaporate. Docs are the durable artifact your CTO, team, or investor actually reads. |
| "Being pragmatic, not dogmatic" | The gate exists because skipping it failed in testing. Pragmatic = 30 minutes of docs vs days of rework. |
| "My six docs are close enough / this set fits better" | The six are canonical. Write each one shorter if needed; never substitute a different document for a canonical slot. |
| "Code already exists, so docs are pointless now" | Docs against existing code still gate every decision not yet made — which is most of them. Write all six against what exists, then continue. |

## Common Mistakes

- **Interviewing instead of drafting.** Users describe faster than they author. Draft first, interview second.
- **One mega-doc.** Six files, not one. Each has a distinct audience and purpose.
- **Skipping the approval turn.** Presenting docs and scaffolding in the same response skips the gate.
- **Letting stack-first thinking skip the PRD.** "React + Node + Postgres" is the Technical Specification, not the PRD. Features and behaviors come first.
