# Product Requirements Document (PRD) - TODO App Upgrade

## 1. Overview

We are upgrading the basic TODO app (currently supporting only `title` and `completed`) to support due dates, priority levels, and filters so users can better organize and prioritize their tasks. The goal is a lean, teachable MVP with no backend changes — all data remains in local storage.

---

## 2. MVP Scope

- **Due dates**: Add an optional `dueDate` field (ISO `YYYY-MM-DD`) to each task; invalid values are treated as absent
- **Priority levels**: Add a `priority` field with enum values `P1 | P2 | P3` (default `P3`), displayed as color-coded badges:
  - P1 → red badge
  - P2 → orange badge
  - P3 → gray badge
- **Filters**: Three tabs — **All**, **Today**, **Overdue**
  - **All**: shows all tasks including completed ones
  - **Today**: shows only incomplete tasks due today
  - **Overdue**: shows only incomplete tasks past their due date
- **Data model validation**:
  - `title`: required
  - `priority`: `"P1" | "P2" | "P3"`, default `"P3"`
  - `dueDate`: optional ISO `YYYY-MM-DD`; invalid values ignored (treated as absent)
- **Storage**: local only — no backend or external storage changes

---

## 3. Post-MVP Scope

- **Overdue highlighting**: Visually highlight overdue tasks in red so they stand out
- **Sorting**: overdue first → priority ascending (P1 → P3) → due date ascending → undated tasks last

---

## 4. Out of Scope

- Notifications
- Recurring tasks
- Multi-user support
- Keyboard navigation / special accessibility features
- External or backend storage
