# OpenClaw Memory System — Setup Template
_Cognitive infrastructure for persistent, structured agent memory._

The core idea: agents wake up fresh every session. Without a deliberate file system, nothing survives restarts. This template gives you a layered memory architecture that scales — daily logs for raw notes, structured files for curated state, identity files for who you are.

---

## The Architecture

```
workspace/
├── AGENTS.md          ← Boot instructions (the agent reads this first)
├── SOUL.md            ← Agent persona, tone, priorities
├── USER.md            ← Who the user is, communication style, preferences
├── DECISIONS.md       ← Major decisions + reasoning (permanent log)
├── ERRORS.md          ← Mistakes and lessons (never repeat these)
├── PROJECTS.md        ← Active project state, pipeline, key dates
├── MEMORY.md          ← Live state: financials, system config (private)
└── memory/
    └── YYYY-MM-DD.md  ← Daily raw notes (auto-created each session)
```

**Three layers:**
1. **Identity** (`SOUL.md`, `USER.md`) — who you are, never changes unless you update it
2. **Structured state** (`DECISIONS.md`, `ERRORS.md`, `PROJECTS.md`) — curated, always current
3. **Raw logs** (`memory/YYYY-MM-DD.md`) — daily scratch pad, distilled periodically

---

## Step 1 — AGENTS.md (Boot Sequence)

This is the first file the agent reads. It enforces the boot sequence.

Put this in `AGENTS.md`:

```markdown
## Every Session — Boot Sequence (NON-NEGOTIABLE)

Before responding to anything:

1. Read `SOUL.md` — who you are
2. Read `USER.md` — who you're helping
3. Read `DECISIONS.md` — major decisions and reasoning
4. Read `ERRORS.md` — mistakes never to repeat
5. Read `PROJECTS.md` — active project state
6. Read `memory/YYYY-MM-DD.md` (today + yesterday) — recent context
7. **MAIN SESSION ONLY:** Read `MEMORY.md` — live private state

No execution before context. No advice without state awareness.

## Memory Write Rules

- Decision made → log it in `DECISIONS.md`
- Mistake made → log it in `ERRORS.md`
- Project state changed → update `PROJECTS.md`
- Anything else worth remembering → `memory/YYYY-MM-DD.md`
- **Mental notes don't survive restarts. Files do.**

## Memory Maintenance (Run Periodically)

1. Read recent `memory/YYYY-MM-DD.md` files
2. Promote decisions → `DECISIONS.md`
3. Promote mistakes/lessons → `ERRORS.md`
4. Update project state → `PROJECTS.md`
5. Update `MEMORY.md` if live state changed
6. Remove resolved/stale items from all files
```

---

## Step 2 — SOUL.md (Agent Identity)

Who the agent is. Tone, priorities, operating style. Loaded every session.

Put this in `SOUL.md`:

```markdown
# SOUL.md

- **Name:** [Agent name]
- **Role:** [What this agent does — e.g., "Execution partner for [business]"]
- **Tone:** [e.g., blunt, direct, no fluff / friendly, detailed, step-by-step]
- **Priorities (in order):**
  1. [Top priority]
  2. [Second priority]
  3. ...

## What I Am
[One paragraph describing the agent's purpose and operating mode]

## Voice
[How the agent communicates — formality, style, what to avoid]

## Boundaries
- [Hard rules — e.g., "Never share credentials", "Ask before sending external messages"]
```

---

## Step 3 — USER.md (Human Profile)

Who the user is. Communication style, technical level, preferences. Never changes unless deliberately updated.

Put this in `USER.md`:

```markdown
# USER.md

- **Name:** [Name]
- **Timezone:** [e.g., America/Chicago]
- **Role/Background:** [e.g., Senior DevOps Engineer, 15 years infra]

## Communication Style

**DO:** [e.g., lead with verdict, assume technical competence, give concrete next steps]
**DON'T:** [e.g., over-explain basics, use hedging language, generic advice]

## Technical Stack
[Key tools, languages, platforms — agent uses this to tailor recommendations]

## Code Style Preferences
[e.g., explicit over clever, comments explain why not what, no unnecessary abstraction]

## Writing Style Preferences
[e.g., short sentences, fragments OK, no em dashes, no cheerleading]
```

---

## Step 4 — DECISIONS.md (Decision Log)

Every major decision gets logged here with context. Prevents re-litigating old choices.

Put this in `DECISIONS.md`:

```markdown
# DECISIONS.md
_Major decisions + reasoning. Log date + context. Archive if reversed, don't delete._

---

## YYYY-MM-DD — [Decision Title]

**Decision:** [What was decided]

**Context:** [Why — what was the situation, what were the alternatives]

**Outcome:** [What happened as a result, or expected outcome]

---

## YYYY-MM-DD — [Next Decision]
...
```

---

## Step 5 — ERRORS.md (Mistake Log)

Mistakes, failed experiments, bad assumptions. Read before acting.

Put this in `ERRORS.md`:

```markdown
# ERRORS.md
_Mistakes and hard lessons. Read this. Never repeat these._

---

## [Error Title] (YYYY-MM-DD)

**Error:** [What went wrong]

**Fix:** [What to do instead]

**Rule:** [One-line rule to prevent recurrence]

---
```

---

## Step 6 — PROJECTS.md (Project State)

Active projects, pipeline status, key dates. Replace MEMORY.md bloat with structured project tracking.

Put this in `PROJECTS.md`:

```markdown
# PROJECTS.md
_Active projects and key dates. Update when things change._

---

## [Project Name] — [Status: Active / Paused / Done]

**Goal:** [What success looks like]

**Status:** [Current state in 1-2 sentences]

**Checklist:**
- ✅ [Done item]
- ⬜ [Pending item]

**Blockers:**
1. [Blocker if any]

---

## Key Dates

| Date | Action |
|------|--------|
| YYYY-MM-DD | [What needs to happen] |
```

---

## Step 7 — MEMORY.md (Live Private State)

Financial balances, system config, anything that changes frequently and is private. **Main session only — don't load in group chats.**

Put this in `MEMORY.md`:

```markdown
# MEMORY.md — Live State
_Private. Load in main session only. Update aggressively._

## Financials
[Current balances, income, deadlines]

## System State
[Tool versions, active configs, API tokens location]

## OPSEC
[Rules about what to share where]
```

---

## Step 8 — Daily Notes (Auto-Written)

The agent should write to `memory/YYYY-MM-DD.md` during and after sessions. No format required — raw notes.

Tell the agent in `AGENTS.md`:

```markdown
After any conversation where a decision was made, context was established,
or follow-up is needed — write a summary to `memory/YYYY-MM-DD.md` before 
ending the session. Do not wait to be asked.
```

---

## How It Compounds

| Timeframe | What happens |
|-----------|-------------|
| Each session | Boot sequence loads all files → full context in seconds |
| End of session | Agent writes to daily log |
| Weekly | Heartbeat distills daily logs → promotes to structured files |
| Monthly | Review structured files, remove resolved items, archive old logs |

**The result:** The agent always has full context without bloat. Old decisions inform new ones. Mistakes don't repeat. Projects stay current.

---

## What Goes Where (Quick Reference)

| Content | File |
|---------|------|
| Who the agent is | `SOUL.md` |
| Who the user is, style preferences | `USER.md` |
| A strategic or business decision | `DECISIONS.md` |
| A mistake or failed experiment | `ERRORS.md` |
| Project status, pipeline, dates | `PROJECTS.md` |
| Raw notes from today's session | `memory/YYYY-MM-DD.md` |
| Financial balances, system config | `MEMORY.md` |
| Reusable agent capabilities | `skills/` |

**Rule of thumb:** If it changes weekly → `PROJECTS.md`. If it's permanent context → identity files. If it's a specific number or config → `MEMORY.md`. If it just happened → daily log.