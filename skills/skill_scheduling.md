
## Trigger
Load this file when the commander requests a new schedule.

---

## Before Building

1. Read `rules.md`, `constraints.md`, `soldiers.md`, `history.md`.
   - If `history.md` does not exist (first run) — skip it and continue without history.
2. Check for expired constraints in `constraints.md` — note them but do not remove without commander approval.
3. Check if `schedule.md` exists:
   - **Does not exist** → create a new schedule file directly, no questions needed.
   - **Exists** → prefer editing it rather than rebuilding from scratch. Unless the user explicitly asked to rebuild from scratch.
     - ⚠️ **אזהרת עלות:** בניית לוז מחדש מאפס דורשת משאבים משמעותיים. האם להמשיך?
     - Wait for explicit confirmation before rebuilding.
4. Identify which rotation is closing this weekend. Check `rules.md`. If unclear, ask: "איזה סבב סוגר בסוף שבוע זה?"
   - ⚠️ "סבב סוגר" תקף **אך ורק** לסוף השבוע שהוגדר במפורש. בתום הסופש כל החיילים חוזרים לזמינות מלאה — אלא אם הוגדר אחרת.
5. Present active constraints summary and ask for confirmation:
   > "לפני שאני בונה — אלה האילוצים הפעילים כרגע: [רשימה]. הכל עדכני?"
6. Inform the commander of expected processing time:
   > "שים לב — בניית לוז שלם לוקחת בדרך כלל 2–5 דקות."
7. Wait for confirmation before proceeding.

---

## Building the Schedule

1. Assign soldiers to shifts respecting:
   - Permitted positions per soldier (`soldiers.md`)
   - All standing rules and personal rules (`rules.md`)
   - All active constraints (`constraints.md`) — including rotation-wide constraints
   - Minimum rest between shifts (from `rules.md`, default 8 hours if undefined)
   - Historical shift load (`history.md`) — prefer soldiers with fewer cumulative shifts

2. Write a reason **only for unusual or non-obvious assignments** — e.g. covering for an absent soldier, exception to a rule, constraint-driven choice. Leave the reason cell empty for standard assignments.

---

## Conflict Handling

If a valid schedule cannot be fully built:
1. Build the best partial schedule possible.
2. Clearly mark unresolved slots with ⚠️.
3. Explain what caused each conflict.
4. Think creatively and generate all possible solutions — not limited to any predefined list. Consider any combination of schedule changes, soldier swaps, shift splits, coverage adjustments, constraint relaxations, or any other approach that could resolve the conflict while minimizing impact on the overall schedule.
5. Present all options to the commander with tradeoffs clearly explained. Do not execute any solution.
6. Ask: "איזו אפשרות לבצע, או יש לך פתרון אחר?"
7. Wait for commander decision before making any change.

---

## Output Format

The schedule uses **one column per position**. Reasons appear only for unusual assignments.

```
# לוז שבועי — [תאריך התחלה] עד [תאריך סיום]

## יום ראשון — DD/MM *(הערת יום אם רלוונטית — סוף שבוע, סבב בבית וכו')*

| שעות        | [עמדה 1]   | [עמדה 2]   | הערות                        |
|-------------|-----------|-----------|------------------------------|
| 06:00–14:00 | שם חייל   | שם חייל   |                              |
| 14:00–22:00 | שם חייל   | שם חייל   | מחליף [שם] שבאילוץ           |
| 22:00–06:00 | שם חייל   | שם חייל   |                              |

## יום שני — DD/MM
...

## סיכום משמרות לחייל

| חייל | משמרות |
|------|--------|
| ...  | ...    |

---

## המלצות
- [חיילים עם עומס גבוה/נמוך במיוחד]
- [עמדות שנראות תת/יתר מאוישות]
- [הצעה קונקרטית להגדיל/להקטין שעות שמירה אם נדרש]
- [תבניות חריגות — למשל אותו חייל תמיד בלילה]

---

## הערות מפקד
[מקום פנוי להערות חופשיות של המפקד על השבוע]
```

---

## Rules Never to Break
- Never assign a soldier to a position not listed in `soldiers.md` unless an explicit temporary override exists in `constraints.md` for that soldier, position, and time period.
- Never ignore an active constraint from `constraints.md`.
- Never skip the active constraints confirmation step.
- Never rebuild the schedule from scratch without first asking the commander.
- Do not write a reason for every assignment — only for exceptions and unusual decisions.