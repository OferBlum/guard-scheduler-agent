# Guard Scheduler — AI-Powered Military Guard Duty Management

> A Claude Code AI agent that manages weekly shift schedules inside an Obsidian workspace. Handles fair assignment, constraint tracking, conflict resolution, and historical records — all through natural-language commands.

---

## Features

- **Automated weekly scheduling** — builds full 7-day shift tables respecting rules, rest periods, and rotation cycles
- **Constraint management** — tracks temporary exemptions, leave, and position overrides with expiry dates
- **Fairness tracking** — maintains cumulative shift counts per soldier across weeks to distribute load equitably
- **Conflict resolution** — flags unresolvable slots with ⚠️, proposes multiple options, and waits for commander approval before acting
- **Incremental editing** — edits the existing schedule rather than rebuilding from scratch, minimizing cost and time
- **Guided onboarding** — walks a new commander through system setup step by step when required files are missing

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| AI Runtime | [Claude Code](https://claude.ai/code) (Anthropic) |
| Agent Instructions | `CLAUDE.md` + modular skill files |
| Workspace | [Obsidian](https://obsidian.md) (Markdown-based) |
| Data Storage | Plain Markdown files (`.md`) |
| Language Model | Claude Sonnet (edits/queries) · Claude Opus (full schedule builds) |

---

## Architecture

The agent uses a **skill-router pattern**: a central `CLAUDE.md` defines the agent's role, scope, and file map, then delegates to a focused skill file based on what the commander requests.

```
CLAUDE.md  ──▶  skills/skill_onboarding.md   (first-time setup)
           ──▶  skills/skill_scheduling.md   (build a weekly schedule)
           ──▶  skills/skill_editing.md      (modify workers/rules/constraints)
           ──▶  skills/skill_history.md      (archive approved schedules)
```

**Data files** (excluded from version control — see `.gitignore`):

| File | Purpose | Written by |
|------|---------|------------|
| `config.md` | Organization settings: language, titles, positions, weekend window, groups | Manager (via agent) |
| `rules.md` | Standing rules: positions, hours, rest, rotation cycles | Manager (via agent) |
| `workers.md` | Workers: name, permitted positions, group, personal rules | Manager (via agent) |
| `constraints.md` | Temporary constraints with expiry dates | Manager (via agent) |
| `schedule.md` | Active weekly schedule | Agent |
| `history.md` | Past schedules + cumulative shift counts | Agent |

See the [`examples/`](examples/) folder for a fully populated demo of all five files with fictional data.

---

## Installation

### Prerequisites

- [Obsidian](https://obsidian.md) installed
- [Claude Code](https://claude.ai/code) CLI or desktop app, connected to the vault folder
- Claude API access (Sonnet or Opus)

### Setup

1. Clone or download this repository.
2. Open the project folder as an Obsidian vault.
3. Open Claude Code in the same directory.
4. Claude Code automatically loads `CLAUDE.md` — the agent is ready.

### First Run (Onboarding)

If `config.md`, `rules.md`, `workers.md`, or `constraints.md` are missing, the agent starts an interactive onboarding:

```
Step 1 — Config:      organization name, language, titles, positions, groups
Step 2 — Rules:       shift hours, rest time, rotation cycles, weekend dates
Step 3 — Workers:     names, permitted positions, group, personal rules
Step 4 — Constraints: active exemptions, leave, overrides — each with an expiry date
Step 5 — Confirm:     agent summarizes all data and waits for approval
```

> The agent writes each answer to the correct file immediately — not at the end of the step.

---

## Usage

### Build a Weekly Schedule

```
"Build a schedule for next week"
```

The agent will:
1. Read rules, constraints, soldiers, and history
2. Identify which rotation is on base this weekend (asks if unclear)
3. Present active constraints for confirmation
4. Warn if a full rebuild is requested (costs more tokens than editing)
5. Build and save the schedule to `schedule.md`

### Edit the Current Schedule

```
"Move [worker] from Tuesday 22:00 to Wednesday 06:00"
"Remove [worker] from Thursday 14:00 shift"
"Who is available for the Monday night shift?"
```

### Manage Workers and Constraints

```
"Add worker: [name], position: operator, rotation 2"
"Add constraint: [name] is exempt from guard duty until 20/05/2026"
"Cancel constraint for [name]"
"Rotation 1 is unavailable all week"
```

### Archive an Approved Schedule

```
"Approved" / "Save to history"
```

The agent appends the week to `history.md` and updates the cumulative shift count table.

---

## Schedule Format

```markdown
# Weekly Schedule — 11/05/2026 to 17/05/2026

## Sunday — 11/05

| Hours       | Shift Manager | Operator     | Notes                        |
|-------------|--------------|--------------|------------------------------|
| 06:00–14:00 | [Worker A]   | [Worker B]   |                              |
| 14:00–22:00 | [Worker C]   | [Worker D]   | Covering for [name] (exempt) |
| 22:00–06:00 | [Worker E]   | [Worker F]   |                              |

...

## Shift Summary

| Worker     | Shifts |
|------------|--------|
| [Worker A] | 2      |
| [Worker C] | 3      |

---

## Recommendations
- Soldiers with unusually high or low load this week
- Patterns worth noting (e.g. same soldier always on night shift)

## Commander Notes
[Free space for the commander's comments]
```

---

## Constraint Types

| Type | Example | Expiry |
|------|---------|--------|
| Full exemption | "[Name] exempt from all guard duty" | Date |
| Time restriction | "Cannot be assigned from Sunday 22:00 through end of Monday" | Date + time |
| Full absence | "Not on base all week" | Date |
| Temporary position | "[Name] authorized to serve as operator until [date]" | Date |
| Rotation-wide | "Rotation 2 unavailable until [date]" | Date |

> **Core principle:** constraints in `constraints.md` always override standing rules in `rules.md`. Constraints are temporary and do not modify permanent rules.

---

## Model Selection Guide

| Task | Recommended Model | Reason |
|------|------------------|--------|
| Questions, onboarding, small edits | **Sonnet** | Fast and cost-efficient |
| Full weekly schedule build from scratch | **Opus** | Higher accuracy justifies the cost |

**Cost tip:** always prefer editing an existing schedule over a full rebuild. A complete rebuild typically takes 2–5 minutes.

---

## Security & Privacy

Personal data (worker names, schedules, constraints, history) is stored in plain Markdown files that are excluded from version control via `.gitignore`. Never commit those files to a public repository. See [`examples/`](examples/) for safe fictional demo data.

---

## Extending the System

| Change | How |
|--------|-----|
| Add a position | Update `rules.md` + `workers.md` |
| Add a standing personal rule | Update `rules.md` and `workers.md` |
| Change weekend hours | Update the "Weekend" section in `rules.md` |
| Add a new skill | Add a file to `skills/` and register it in the Skills table in `CLAUDE.md` |

---

## Known Limitations

- The agent responds only to shift scheduling requests — all other requests are politely declined.
- No graphical interface — all interaction is text-based inside Claude Code.
- `history.md` grows over time; old weeks can be manually archived if the file becomes large.

---

*Built with [Claude Code](https://claude.ai/code) · Anthropic*
