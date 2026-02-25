# Claude Code Memory System — Setup Template
_Cognitive infrastructure for persistent, structured agent memory in Claude Code._

Claude Code starts fresh every session. Without a deliberate file system, nothing survives restarts. This template gives you a layered memory architecture — daily logs for raw notes, structured files for curated state, identity files for who you are and how you work.

---

## The Architecture

```
project/ (or ~/.claude/ for global config)
├── CLAUDE.md          ← Boot instructions (Claude reads this automatically)
├── SOUL.md            ← Agent persona, tone, priorities
├── USER.md            ← Who you are, communication style, code preferences
├── DECISIONS.md       ← Major decisions + reasoning (permanent log)
├── ERRORS.md          ← Mistakes and lessons (never repeat these)
├── PROJECTS.md        ← Active project state, pipeline, key dates
├── MEMORY.md          ← Live state: config, private context (optional)
└── memory/
    └── YYYY-MM-DD.md  ← Daily raw notes (written during/after sessions)
```

**Two placement options:**
- `~/.claude/CLAUDE.md` — global, applies to every Claude Code session on your machine
- `./CLAUDE.md` in a project root — project-scoped, only applies in that directory

**Three layers:**
1. **Identity** (`SOUL.md`, `USER.md`) — stable context, loaded every session
2. **Structured state** (`DECISIONS.md`, `ERRORS.md`, `PROJECTS.md`) — curated, always current
3. **Raw logs** (`memory/YYYY-MM-DD.md`) — daily scratch pad, distilled periodically

---

## Step 1 — CLAUDE.md (Boot Sequence)

Claude Code reads `CLAUDE.md` automatically at session start. This is where you enforce the boot sequence and write rules.

Put this in `CLAUDE.md`:

```markdown
## Session Boot Sequence (NON-NEGOTIABLE)

Before responding to anything, read these files in order:

1. Read `SOUL.md` — who you are and how you operate
2. Read `USER.md` — who you're helping, their style and preferences
3. Read `DECISIONS.md` — major decisions already made, don't re-litigate
4. Read `ERRORS.md` — mistakes never to repeat
5. Read `PROJECTS.md` — active project state and priorities
6. Read `memory/YYYY-MM-DD.md` for today and yesterday — recent context
7. Read `MEMORY.md` if it exists — live private state

No execution before context. No advice without state awareness.

## Memory Write Rules

- Decision made → log it in `DECISIONS.md`
- Mistake made → log it in `ERRORS.md`  
- Project state changed → update `PROJECTS.md`
- Anything else worth remembering → `memory/YYYY-MM-DD.md`
- **Mental notes don't survive restarts. Files do.**

## End of Session

After any conversation where a decision was made, context was established,
or follow-up is needed — write a summary to `memory/YYYY-MM-DD.md` before
ending. Do not wait to be asked.

## Periodic Maintenance

Every few sessions, run a memory hygiene pass:
1. Read recent `memory/YYYY-MM-DD.md` files
2. Promote decisions → `DECISIONS.md`
3. Promote mistakes/lessons → `ERRORS.md`
4. Update project state → `PROJECTS.md`
5. Remove resolved/stale items from all files
```

---

## Step 2 — SOUL.md (Agent Identity)

Who the agent is. Tone, priorities, operating style. Loaded every session.

Put this in `SOUL.md`:

```markdown
# SOUL.md

- **Name:** [Agent name or just "Claude"]
- **Role:** [What this agent does — e.g., "DevOps copilot for [project]"]
- **Tone:** [e.g., blunt, direct, no fluff / detailed, step-by-step]
- **Priorities (in order):**
  1. [Top priority]
  2. [Second priority]
  3. ...

## What I Am
[One paragraph describing operating mode and purpose]

## Voice
[Communication style — formality, what to avoid, how to format responses]

## Boundaries
- [Hard rules — e.g., "Ask before running destructive commands"]
- [e.g., "Never share credentials in output"]
```

---

## Step 3 — USER.md (Human Profile)

Who the user is. Communication style, technical level, code and writing preferences.

Put this in `USER.md`:

```markdown
# USER.md

- **Name:** [Name]
- **Timezone:** [e.g., America/Chicago]
- **Background:** [e.g., Senior DevOps Engineer, 15 years infrastructure]

## Communication Style

**DO:** [e.g., lead with verdict, assume technical competence, concrete next steps]
**DON'T:** [e.g., over-explain basics, hedge without specifics, motivational filler]

## Technical Stack
[Key tools, languages, platforms, cloud providers]

## Code Style Preferences
[e.g., explicit over clever, comments explain why not what, prefer functions over classes for utilities]

## Writing Style Preferences
[e.g., short sentences, fragments OK, no em dashes, no exclamation marks]

## Review Preferences
[e.g., flag anything that adds abstraction without clear benefit, always suggest the simpler path first]
```

---

## Step 4 — DECISIONS.md (Decision Log)

Every major decision gets logged with context and date. Prevents re-litigating old choices.

Put this in `DECISIONS.md`:

```markdown
# DECISIONS.md
_Major decisions + reasoning. Log date + context. Archive if reversed, never delete._

---

## YYYY-MM-DD — [Decision Title]

**Decision:** [What was decided]

**Context:** [Why — situation, alternatives considered]

**Outcome:** [What happened, or expected result]

---
```

---

## Step 5 — ERRORS.md (Mistake Log)

Mistakes, bad assumptions, failed experiments. Read before acting.

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

Active projects, status, pipeline, key dates. Keeps MEMORY.md lean.

Put this in `PROJECTS.md`:

```markdown
# PROJECTS.md
_Active projects and key dates. Update when things change._

---

## [Project Name] — [Status]

**Goal:** [What success looks like]

**Status:** [Current state in 1-2 sentences]

**Checklist:**
- ✅ [Done]
- ⬜ [Pending]

**Blockers:** [Any blockers]

---

## Key Dates

| Date | Action |
|------|--------|
| YYYY-MM-DD | [What needs to happen] |
```

---

## Step 7 — MEMORY.md (Live Private State)

System config, private context, anything that changes frequently. Keep it lean.

Put this in `MEMORY.md`:

```markdown
# MEMORY.md — Live State
_Load every session. Update aggressively._

## System State
[Tool versions, active configs, environment details]

## Private Context
[Anything sensitive that shouldn't be in shared files]
```

---

## Step 8 — Daily Notes

The agent writes to `memory/YYYY-MM-DD.md` during and after sessions. No strict format needed — raw notes that capture what happened, what was decided, what to follow up on.

The `CLAUDE.md` boot sequence instruction handles this automatically.

---

## Global vs Project Scope

**Global (`~/.claude/CLAUDE.md`):**
Use for preferences and identity that apply everywhere — your communication style, code style, universal rules. `USER.md`, `SOUL.md`, and `ERRORS.md` are good candidates for global scope.

**Project (`./CLAUDE.md`):**
Use for project-specific context — active decisions, current state, project-scoped mistakes. `DECISIONS.md`, `PROJECTS.md`, and daily logs belong here.

You can have both — Claude Code merges them, with project-level taking precedence.

---

## How It Compounds

| Timeframe | What happens |
|-----------|-------------|
| Each session | Boot sequence loads all files → full context in seconds |
| End of session | Agent writes to daily log |
| Weekly | Manual or prompted distillation → promote to structured files |
| Monthly | Review structured files, remove resolved items, archive old logs |

---

## What Goes Where — Quick Reference

| Content | File |
|---------|------|
| Agent persona, tone, priorities | `SOUL.md` |
| Your style, stack, preferences | `USER.md` |
| A strategic or technical decision | `DECISIONS.md` |
| A mistake or failed experiment | `ERRORS.md` |
| Project status, pipeline, dates | `PROJECTS.md` |
| Raw notes from today | `memory/YYYY-MM-DD.md` |
| System config, private context | `MEMORY.md` |

**Rule of thumb:** If it changes weekly → `PROJECTS.md`. If it's who you are → identity files. If it just happened → daily log. If it's a hard lesson → `ERRORS.md`.