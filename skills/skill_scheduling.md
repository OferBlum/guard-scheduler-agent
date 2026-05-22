
## Trigger
Load this file when the manager requests a new schedule.

---

## Before Building

1. Read `config.md`, `rules.md`, `constraints.md`, `workers.md`, `history.md`.
   - If `history.md` does not exist (first run) — skip it and continue without history.
2. Check for expired constraints in `constraints.md` — note them but do not remove without manager approval.
3. Check if `schedule.md` exists:
   - **Does not exist** → create a new schedule file directly, no questions needed.
   - **Exists** → prefer editing it rather than rebuilding from scratch. Unless the user explicitly asked to rebuild from scratch.
     - ⚠️ Warn the manager: rebuilding from scratch requires significant resources. Ask for explicit confirmation before proceeding.
     - Wait for explicit confirmation before rebuilding.
4. If groups are enabled (`config.md` → `group_type` is not false): identify which group is on weekend duty this week and the weekend window. Check `rules.md`. If unclear, ask the manager.
   - ⚠️ A group's weekend duty applies **only** to the explicitly defined weekend window. After the weekend ends, all workers return to full availability — unless otherwise specified.
5. Present active constraints summary and ask for confirmation before building.
6. Inform the manager that building a full schedule typically takes 2–5 minutes.
7. Wait for confirmation before proceeding.

---

## Building the Schedule

1. Assign workers to shifts respecting:
   - Permitted positions per worker (`workers.md`)
   - All standing rules and personal rules (`rules.md`)
   - All active constraints (`constraints.md`) — including group-wide constraints
   - Minimum rest between shifts (from `rules.md`, default 8 hours if undefined)
   - Historical shift load (`history.md`) — prefer workers with fewer cumulative shifts

2. Write a reason **only for unusual or non-obvious assignments** — e.g. covering for an absent worker, exception to a rule, constraint-driven choice. Leave the reason cell empty for standard assignments.

---

## Conflict Handling

If a valid schedule cannot be fully built:
1. Build the best partial schedule possible.
2. Clearly mark unresolved slots with ⚠️.
3. Explain what caused each conflict.
4. Think creatively and generate all possible solutions — not limited to any predefined list. Consider any combination of schedule changes, worker swaps, shift splits, coverage adjustments, constraint relaxations, or any other approach that could resolve the conflict while minimizing impact on the overall schedule.
5. Present all options to the manager with tradeoffs clearly explained. Do not execute any solution.
6. Ask the manager to choose an option or propose their own.
7. Wait for manager decision before making any change.

---

## Output Format

The schedule uses **one column per position**. Reasons appear only for unusual assignments.
Use the position names from `rules.md`. Use the configured language for all labels and text.

```
# Weekly Schedule — [Start Date] to [End Date]

## [Day name] — DD/MM  *(day note if relevant — weekend, group on leave, etc.)*

| Hours       | [Position 1] | [Position 2] | Notes                          |
|-------------|--------------|--------------|--------------------------------|
| 06:00–14:00 | Worker name  | Worker name  |                                |
| 14:00–22:00 | Worker name  | Worker name  | Covering for [name] (exempt)   |
| 22:00–06:00 | Worker name  | Worker name  |                                |

## [Next day] — DD/MM
...

## Shift Summary per Worker

| Worker | Shifts |
|--------|--------|
| ...    | ...    |

---

## Recommendations
- [Workers with unusually high or low load]
- [Positions that appear understaffed or overstaffed]
- [Concrete suggestion to adjust hours if needed]
- [Unusual patterns — e.g. same worker always on nights]

---

## Manager Notes
[Space for the manager's free-form notes about the week]
```

---

## Rules Never to Break
- Never assign a worker to a position not listed in `workers.md` unless an explicit temporary override exists in `constraints.md` for that worker, position, and time period.
- Never ignore an active constraint from `constraints.md`.
- Never skip the active constraints confirmation step.
- Never rebuild the schedule from scratch without first asking the manager.
- Do not write a reason for every assignment — only for exceptions and unusual decisions.
