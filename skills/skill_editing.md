
## Trigger
Load this file when the commander requests any edit — to the schedule, soldiers, rules, or constraints.

---

## Edit Types

### עריכת לוז
- "העבר את [שם] מ[יום/שעה] ל[יום/שעה]" → update `schedule.md`
- "הסר את [שם] ממשמרת [יום/שעה]" → update `schedule.md`, mark slot as open ⚠️
- "מי פנוי ל[יום/שעה]?" → check `soldiers.md` + `constraints.md` + `schedule.md` and suggest available soldiers

### עריכת אנשים
- "הוסף חייל [שם]" → ask for permitted positions and personal rules, then update `soldiers.md`
- "עדכן עמדות של [שם]" → update `soldiers.md`
- "הסר חייל [שם]" → confirm with commander, then remove from `soldiers.md` and flag any affected shifts in `schedule.md`

### עריכת חוקים
- "הוסף חוק: [תיאור]" → update `rules.md`, confirm with commander
- "בטל חוק: [תיאור]" → confirm with commander before removing

### עריכת אילוצים
- "הוסף אילוץ: [שם] פטור עד [תאריך] (שעה אופציונלית)" → update `constraints.md` with date and time if provided
- "בטל אילוץ של [שם]" → remove from `constraints.md`, confirm with commander
- "תן ל[שם] לשמור ב[עמדה] עד [תאריך] (שעה אופציונלית)" → add a temporary position override to `constraints.md` with expiry date and time if provided
- "סבב [מספר] לא זמין עד [תאריך]" → add a rotation-wide constraint to `constraints.md` — applies to all soldiers in that rotation

Every constraint in `constraints.md` must include:
- Soldier name **or** rotation number (for rotation-wide constraints)
- Constraint type (exemption / position override / rotation-wide)
- Expiry date
- Expiry time — if provided, otherwise constraint expires at end of expiry date

---

## After Every Edit
1. State exactly what was changed.
2. Flag any downstream effects (e.g. removed soldier leaves an open shift).
3. Ask if further action is needed.

## Rules
- Never modify `rules.md` without explicit commander instruction.
- Always confirm destructive actions (removing a soldier, canceling a rule) before executing.
- When a schedule edit is requested — **edit the existing `schedule.md`** rather than rebuilding the schedule from scratch. Rebuilding consumes significant tokens and time.