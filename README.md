# founder-skill

**A hard-gate skill for AI coding agents: no application code until the six-document Specification Package exists and is approved.**

`founder-skill` makes any AI coding agent (OpenCode, Claude Code) stop, draft a complete spec package from your brief, get your sign-off, and only then start scaffolding. Specs are the fast path, not overhead — every assumption you skip is rework you pay later.

## Why

AI agents under deadline pressure ("demo in 2 days, just get something working") will skip planning, scaffold immediately, and bury undocumented assumptions in code. This skill was written and tested against exactly that failure mode:

- **RED (baseline):** agents skipped all docs under time pressure, obeyed "skip the docs" requests, and retrofitted substitute documents from already-written code
- **GREEN:** with the skill loaded, agents draft all six documents first and refuse to scaffold until approved
- **REFACTOR:** the canonical six are locked — agents can't swap a document for an "equivalent"

## The Gate

Refuse to create application code (scaffolding, `package.json`, server files, schema DDL, components, routes, seed scripts) until `docs/specs/` contains all six documents and the user has approved them.

**Allowed before approval:** writing/updating the six docs, environment probes, reading existing files.

## The Specification Package

| # | Document | File | Answers |
|---|----------|------|---------|
| 1 | Product Requirements Document (PRD) | `docs/specs/01-prd.md` | Functional scope, feature-level behaviors, business objectives |
| 2 | Technical Specification | `docs/specs/02-technical-spec.md` | Infrastructure stack, architectural decisions |
| 3 | User Flow Document | `docs/specs/03-user-flow.md` | Primary user journeys, interaction triggers, page transitions |
| 4 | Design System Guidelines | `docs/specs/04-design-system.md` | Color palette, typography, UI component parameters |
| 5 | Data Model & Access Control Document | `docs/specs/05-data-model-rbac.md` | Relational data models, RBAC matrix, storage configuration |
| 6 | Project Delivery Plan | `docs/specs/06-project-plan.md` | Phased timeline, build sequence, post-launch monitoring |

Documents are created in order — each feeds the next.

## Compliance Layer

Legal, privacy, and accessibility requirements are answered **inside the existing six — never as a seventh document** (a conditional seventh doc would let agents rationalize skipping it):

- **PRD** picks up the driving inputs: target jurisdictions, under-13 audience, business model, marketing email
- **Design System Guidelines** carries WCAG 2.1 AA (4.5:1 contrast, focus states, alt text) and font/image license provenance
- **Data Model & Access Control** carries data minimization (purpose + retention per field), SDK/sub-processor inventory, lawful basis, deletion path
- **Project Delivery Plan** ends with a **Launch Readiness Gate** — always-on items (privacy policy before first email field, ToS, footer identity, unsubscribe, WCAG funnel pass, no fake reviews/hidden fees/unsupported claims) plus conditional annexes (EU cookie banner + 14-day withdrawal, COPPA escalation, all-in pricing)

## Workflow (Hybrid)

1. **Collect the brief.** Use the user's description; ask one focused round of questions if essentials are missing.
2. **Draft all six** under `docs/specs/` with sensible defaults, marking uncertain choices `> DECISION NEEDED: ...`.
3. **Interview to fill gaps.** Walk the user through only the `DECISION NEEDED` items.
4. **Approval gate.** Present a one-paragraph summary per doc and ask for approval of all six. No coding in the same turn.
5. **Build.** Only after approval, implement per the Project Delivery Plan.

## Install

**OpenCode:**

```bash
git clone https://github.com/Himath-Rajapaksha/founder-skill.git
mkdir -p ~/.config/opencode/skills/founder-skill
cp founder-skill/skills/founder-skill/SKILL.md ~/.config/opencode/skills/founder-skill/
```

**Claude Code:**

```bash
mkdir -p ~/.claude/skills/founder-skill
cp founder-skill/skills/founder-skill/SKILL.md ~/.claude/skills/founder-skill/
```

The skill triggers automatically when you start a new web app or project from scratch, when about to skip planning under time pressure, or when the user asks to skip planning docs.

## What It Resists

The skill ships with a rationalization table and red-flag list counters for the excuses agents actually used during testing:

| Excuse | Reality |
|--------|---------|
| "Demo/deadline in N days — defaults are correct" | Drafting the package takes under 30 minutes; a wrong default discovered mid-build costs days |
| "User explicitly said no planning docs" | Present the gate once, then draft all six so review is one pass |
| "Simple CRUD doesn't need this" | Simple apps have the most undocumented assumptions |
| "I'll write the docs after the code" | Reverse-engineered docs can't gate decisions already made |
| "I already scaffolded — too late" | Sunk cost — write the six against what exists, then continue |
| "My six docs are close enough" | The six are canonical; write shorter, never substitute |

## License

MIT
