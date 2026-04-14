# 🏁 Frontend Development Race — Round 2
## "Debug & Complete" Challenge

---

### ⏱ Time Limit: 45 Minutes

---

## Overview

You've been handed the source code for **TaskFlow** — a multi-page task management web app. The previous developer left in a hurry. The site opens in a browser but is full of bugs and missing pieces.

Your job is to **find and fix the bugs**, **complete missing functionality**, and **polish the UI** so TaskFlow works correctly and looks great.

You will be judged **entirely on what you can see and interact with in the browser**. No one reads your code.

---

## The App: TaskFlow

TaskFlow is a 4-page website:

| Page | File | Purpose |
|------|------|---------|
| **Dashboard** | `index.html` | Overview stats, recent tasks, activity feed |
| **Task Board** | `tasks.html` | Kanban board — create, complete, delete tasks |
| **Archive** | `archive.html` | View and restore archived tasks |
| **Settings** | `settings.html` | Profile, notifications, data management |

Shared files:
- `css/style.css` — global layout and components
- `css/pages.css` — page-specific styles
- `js/app.js` — shared state, localStorage, utilities
- `js/ui.js` — page-specific interactivity

---

## What You Must Fix & Complete

### ✅ Functional Requirements

| # | Page | Requirement |
|---|------|-------------|
| F1 | All | Sidebar navigation links navigate to the correct page |
| F2 | tasks.html | "+ New Task" button opens the modal; submitting adds the card to the correct priority column |
| F3 | tasks.html | Form validates that **both** title and priority are filled before submission |
| F4 | tasks.html | "✔ Done" button marks a task complete; "Undo" reverses it — without corrupting any other tasks |
| F5 | tasks.html | "🗑 Delete" removes **only** the clicked task |
| F6 | tasks.html | Filter buttons (All / Pending / Done) correctly show the right subset **without corrupting task state** |
| F7 | tasks.html | Search bar filters tasks in real time |
| F8 | index.html | Stats (Total, Completed, Pending, Progress %) are accurate and update when tasks change |
| F9 | index.html | Progress bar fill grows and shrinks with the completion percentage |
| F10 | tasks.html | Pressing Escape closes the open modal |
| F11 | settings.html | Clicking settings tab items (Profile, Notifications, etc.) shows the correct panel |
| F12 | All | Tasks created on tasks.html are still visible when you navigate to index.html (persist across pages) |

### 🎨 UI / Visual Requirements

| # | Page | Requirement |
|---|------|-------------|
| U1 | All | Topbar buttons have proper spacing from the right edge |
| U2 | tasks.html | Three kanban columns are visually distinct (separated by headers, borders, or backgrounds) |
| U3 | All | The site uses a clean sans-serif font (not browser default serif) |
| U4 | tasks.html | The "New Task" modal is centred **both horizontally and vertically** on screen |
| U5 | index.html | All four stat cards fit on screen without horizontal overflow (desktop) |
| U6 | tasks.html | Controls row (search + filter pills) wraps gracefully on narrower screens |
| U7 | tasks.html | Long task titles are truncated with an ellipsis instead of overflowing the card |
| U8 | All | Due dates are displayed in a consistent, readable format |

### 📱 Responsiveness Requirements

| # | Requirement |
|---|-------------|
| R1 | No page requires horizontal scrolling on any screen size |
| R2 | Task board stacks to a single column on mobile screens (≤ 768px) |
| R3 | Stat cards display in 2 columns on tablet/mobile |

---

## Bonus Features (Optional — Extra Marks)

Judged on visible result only.

| Bonus | Description |
|-------|-------------|
| B1 | Column task-count badges on the kanban board update dynamically |
| B2 | Overdue task cards are visually distinguished (e.g. red due date) |
| B3 | Smooth animations when cards are added or removed |
| B4 | Sidebar / navigation is accessible on mobile (hamburger toggle or similar) |
| B5 | Archive page is fully functional — tasks can be archived from the board and restored from the archive |

---

## Tips

- Open **DevTools → Console** (F12) — JavaScript errors will point you to broken code.
- Check **all four pages**, not just tasks.html.
- Test navigation links early — broken links will block you from seeing other bugs.
- Try adding a task, then navigating to the Dashboard. Do your stats update?
- Resize the browser window to spot responsiveness issues.
- Fix **functional bugs first**, then polish the UI.

**Good luck! ⚡**
