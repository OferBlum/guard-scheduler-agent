
## Trigger
Load this file when the manager requests any edit.

---

## What Can Be Edited

Anything — `config.md`, `rules.md`, `workers.md`, `constraints.md`, `schedule.md`, `history.md`, or how the schedule looks and is formatted. The manager decides what to change.

---

## How to Handle Any Edit Request

1. Understand exactly what the manager wants to change.
2. If it's destructive (removing a worker, canceling a rule, clearing history) — confirm before executing.
3. Make the change in the relevant file(s).
4. State what was changed.
5. Flag any downstream effects (e.g. removing a worker leaves open shifts).
6. Ask if further action is needed.

---

## Constraint Rules

Every constraint in `constraints.md` must include:
- Worker name **or** group identifier
- Constraint type (exemption / position override / group-wide)
- Expiry date and time (time optional — defaults to end of day)

---

## One Hard Rule

When a schedule change is requested — **edit `schedule.md` directly** rather than rebuilding from scratch. Rebuilding costs significant time and tokens.
