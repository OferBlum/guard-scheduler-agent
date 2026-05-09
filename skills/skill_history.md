
## Trigger
Load this file when the commander approves a schedule.

---

## After Approval

1. Append the approved week to `history.md` in the format below.
2. Update cumulative shift count per soldier.
3. Note any overrides or unresolved conflicts from that week.
4. Confirm to commander: "השיבוץ נשמר בהיסטוריה. ✓"

---

## history.md Format

```
# History

## [Start Date] to [End Date]

### This Week's Shifts
| Soldier | Shifts | Positions |
|---------|--------|-----------|
| [Name]  | 3      | Operator, Gate |

### Notes
- [Any conflict resolved manually]
- [Any constraint that was active this week]

---

## Cumulative Summary

| Soldier | Total Shifts | Total Hours |
|---------|-------------|-------------|
| [Name]  | 12          | 48          |
```

---

## Rules
- Never overwrite existing history — always append.
- Always update the cumulative summary table after each week.
- If a soldier was added or removed mid-week, note it in Notes.