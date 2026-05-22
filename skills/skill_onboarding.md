
## Trigger
Load this file when `config.md` or any of the required files are missing: `rules.md`, `workers.md`, `constraints.md`.

## Behavior
Guide the manager through setup one step at a time. Do not ask multiple questions at once. Wait for the answer before moving to the next question.

**After every answer — write the information to the correct file immediately. Do not wait until the end of the step.**

---

## Step 0 — Language First

Before anything else, ask:

> "What language should I use? / באיזו שפה לדבר? / ¿En qué idioma prefieres? / Quelle langue préférez-vous?"

Write the answer to `config.md` → `language` immediately.
**From this point on, conduct the entire onboarding in the configured language.**

Then continue asking (one at a time, in the configured language):
1. What is your organization's name?
2. What is your title? (e.g. Commander, Manager, Supervisor, Shift Lead)
3. What do you call the people you schedule? (e.g. Guard, Employee, Soldier, Nurse, Technician)
4. Does your organization use named groups (rotations, crews, teams, squads)? If yes, what are they called?

Write each answer to `config.md` immediately. Confirm before moving to Step 1.

---

## Step 1 — rules.md

Ask one at a time (in the configured language):

1. What positions (posts, roles, or stations) exist in your organization? List their names.
2. For each position — what are the shift hours? How many workers are required per shift? Any other details?
3. What is the minimum rest time between shifts for a worker?
4. Is there a maximum number of shifts a worker can do per week?
5. When does your weekend / time-off window start? (day and time, e.g. "Friday 14:00")
6. When does it end? (day and time, e.g. "Sunday 06:00")
7. If groups are enabled: how many groups exist? What is each group named?
8. Which group is on weekend duty this week?
9. Are there any other general rules?

→ Write each answer to `rules.md` immediately — not at the end of the step.
→ Confirm with the manager before moving to the next step.

---

## Step 2 — workers.md

Ask (in the configured language):

1. List all workers (can be provided as a bulk list).
2. For each worker — which positions are they permitted to work?
3. If groups are enabled: which group is each worker in?
4. Does any worker have permanent personal rules?

**Details required per worker:**
- Full name
- Permitted positions (from the list defined in Step 1)
- Group name or number (if groups are enabled)
- Permanent personal rules — if any (e.g. "weekends only", "no night shifts")

→ Write each worker to `workers.md` immediately upon receiving their details.
→ Permanent personal rules — also add to `rules.md` under a "Personal Rules" section.
→ Confirm with the manager before moving to the next step.

---

## Step 3 — constraints.md

Ask (in the configured language):

1. Are there any active temporary constraints right now? (exemptions, leave, restrictions with an end date)
2. Is there a constraint on an entire group? (e.g. "Group 2 unavailable all week")

**Possible constraint types:**
- Individual worker — exemption, time restriction, specific position, defined period
- Entire group — all workers in the group unavailable for a period

→ If yes — create `constraints.md` with details and expiry dates. Write each constraint immediately.
→ If no — create an empty `constraints.md`.

---

## Step 4 — Confirm

Summarize all files back to the manager in the configured language.
Ask: "Does everything look correct? Ready to build the first schedule."
