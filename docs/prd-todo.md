# Product Requirements Document (PRD) - TODO App Upgrade

## 1. Overview

Upgrade the basic TODO app with optional due dates, priority levels, and date-based filters so
users can identify and organize urgent tasks. Keep the MVP simple and teachable, with task data
stored locally and no backend changes.

Sources: [Requirements meeting](artifacts/09162025-requirements-meeting.vtt) and
[scope confirmation](artifacts/09172025-slack-conversation-export.txt). The later scope
confirmation places overdue highlighting and the proposed sorting rules in Post-MVP.

---

## 2. MVP Scope

- Retain the basic task model, including a required `title` and completion status.
- Allow an optional `dueDate` in ISO `YYYY-MM-DD` format. Ignore invalid values and treat them as
  absent.
- Support `priority` values `P1`, `P2`, and `P3`, defaulting to `P3` when no priority is supplied.
- Display priority as a color-coded badge: red for `P1`, orange for `P2`, and gray for `P3`.
  The meeting requested these badges; the later scope confirmation did not explicitly defer them.
- Provide **All**, **Today**, and **Overdue** filters, preferably as tabs:
  - **All** shows both completed and incomplete tasks.
  - **Today** shows incomplete tasks due today.
  - **Overdue** shows incomplete tasks with a due date before today.
  - Tasks without a valid due date do not appear in Today or Overdue.
- Keep task storage local; do not make backend changes or use external storage.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks, for example in red.
- Sort tasks using the proposed ordering: overdue first, then priority (`P1` to `P3`), then due
  date ascending, with undated tasks last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user functionality.
- Additional keyboard navigation or special accessibility features for this upgrade; this does not
  call for removing existing accessibility support.
- Backend changes and external storage; storage remains local.