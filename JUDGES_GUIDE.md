# 🔒 JUDGES' GUIDE — TaskFlow Multi-Page Debug Round
### ⚠️ DO NOT DISTRIBUTE TO PARTICIPANTS

---

## File Structure

```
taskflow/
├── index.html        (Dashboard)
├── tasks.html        (Task Board — main interactive page)
├── archive.html      (Archived tasks)
├── settings.html     (Settings)
├── css/
│   ├── style.css     (Global styles, layout, components)
│   └── pages.css     (Page-specific styles)
└── js/
    ├── app.js        (Shared state, storage, utilities)
    └── ui.js         (Page-specific UI logic)
```

---

## Complete Bug Registry (20 Bugs)

---

### 🗂 Category A — HTML Bugs (across pages)

**BUG 1 — Missing viewport meta tag** *(All 4 HTML files, `<head>`)*
- All four pages are missing `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- **Effect:** Pages render at desktop width on mobile — requires horizontal scrolling.
- **Fix:** Add viewport meta tag to every page's `<head>`.
- **File:** `index.html`, `tasks.html`, `archive.html`, `settings.html`
- **Rubric:** R1

---

**BUG 2 — Nav links missing `.html` extension** *(All 4 HTML files, sidebar `<a>` tags)*
- Links use `href="index"`, `href="tasks"` etc. without `.html`.
- **Effect:** Clicking nav links navigates to 404 / broken URLs (unless on a web server that rewrites them).
- **Fix:** Change all hrefs to `index.html`, `tasks.html`, `archive.html`, `settings.html`.
- **File:** All HTML files
- **Rubric:** F-Nav

---

**BUG 3 — Progress bar fill element missing** *(index.html, dashboard stat card)*
- The `.progress-fill` CSS and JS logic both exist, but the `<div class="progress-fill">` element is absent from the HTML.
- **Effect:** Progress bar track shows but never fills.
- **Fix:** Add `<div class="progress-fill"></div>` inside `.progress-wrap`.
- **File:** `index.html`
- **Rubric:** F9 (stats visual)

---

**BUG 4 — Board column wrappers have no class** *(tasks.html, `.board` children)*
- The three `<div>` columns inside `.board` have no class. The CSS `.board { display:grid; grid-template-columns: repeat(3,1fr) }` still applies since it targets direct children — but without a column class, no column-specific background, border-radius, or header styles are applied, making columns appear visually flat and un-separated.
- **Fix:** Add `class="task-col"` (or any class) to each wrapper `<div>` and add matching background/border styles.
- **File:** `tasks.html`
- **Rubric:** U2

---

**BUG 5 — Settings tab switcher uses assignment instead of equality** *(js/ui.js, `initSettingsPage`)*
- `p.dataset.panel = target` (assignment) instead of `p.dataset.panel === target` (comparison).
- **Effect:** Clicking any settings tab shows/hides all panels incorrectly — all panels end up set to the same dataset value.
- **Fix:** Change `=` to `===`.
- **File:** `js/ui.js`
- **Rubric:** F-Settings

---

**BUG 6 — Submit button ID mismatch** *(tasks.html + js/ui.js)*
- The button in HTML has `id="save-task"`, but `ui.js` adds its event listener to `document.getElementById('save-tasks')` (with an `s`).
- **Effect:** Clicking "Add Task" does nothing — no listener is attached.
- **Fix:** Either change the HTML id to `save-tasks`, or change the JS selector to `save-task`.
- **File:** `tasks.html`, `js/ui.js`
- **Rubric:** F2

---

### 🎨 Category B — CSS Bugs

**BUG 7 — Font family never declared** *(css/style.css, `:root`)*
- The `font-family` declaration is present but commented out in `:root` and never applied to `body`.
- **Effect:** Browser falls back to serif (Times New Roman) — the entire site looks unstyled.
- **Fix:** Uncomment or add `font-family: 'DM Sans', system-ui, sans-serif;` to `body`.
- **File:** `css/style.css`
- **Rubric:** U3

---

**BUG 8 — Topbar only has left-side padding** *(css/style.css, `.topbar`)*
- `padding: 0 0 0 1.8rem` — only the left is padded. The right side has 0 padding.
- **Effect:** Topbar action buttons clip flush against the right edge of the screen.
- **Fix:** Change to `padding: 0 1.8rem` (or `padding: 0 1.8rem 0 1.8rem`).
- **File:** `css/style.css`
- **Rubric:** U1

---

**BUG 9 — Stats grid uses fixed pixel column widths** *(css/style.css, `.stats-grid`)*
- `grid-template-columns: 220px 220px 220px 220px` overflows on viewports narrower than ~920px.
- **Fix:** Change to `grid-template-columns: repeat(4, 1fr)`.
- **File:** `css/style.css`
- **Rubric:** U5, R3

---

**BUG 10 — Sidebar overflow set to `scroll` (always shows scrollbar)** *(css/style.css, `.sidebar`)*
- `overflow-y: scroll` forces a scrollbar to always appear, even when content fits.
- **Fix:** Change to `overflow-y: auto`.
- **File:** `css/style.css`
- **Rubric:** U-Polish

---

**BUG 10b — `.tasks-controls` missing `flex-wrap`** *(css/pages.css, `.tasks-controls`)*
- No `flex-wrap: wrap` — search bar and filter pills overflow on narrow screens.
- **Fix:** Add `flex-wrap: wrap;`.
- **File:** `css/pages.css`
- **Rubric:** R1, U6

---

**BUG 11 — Task card has no priority left-border colour** *(css/pages.css, `.task-card`)*
- The `.task-card` has no `border-left` declaration. There is no CSS rule applying `border-left-color` based on priority class.
- **Effect:** All task cards look the same — no visual priority indicator.
- **Fix:** Add `border-left: 3px solid transparent;` to `.task-card`, then:
  ```css
  .task-card.priority-high   { border-left-color: var(--danger); }
  .task-card.priority-medium { border-left-color: var(--warn); }
  .task-card.priority-low    { border-left-color: var(--success); }
  ```
  (Note: the JS does set a `priority-*` class on each card via `buildCard()`.)
- **File:** `css/pages.css`
- **Rubric:** U-Cards

---

**BUG 11b — Task card title missing truncation properties** *(css/pages.css, `.task-card-title`)*
- `text-overflow: ellipsis` is set but `overflow: hidden` and `white-space: nowrap` are both absent.
- **Effect:** Long titles overflow the card instead of truncating.
- **Fix:** Add `overflow: hidden; white-space: nowrap;`.
- **File:** `css/pages.css`
- **Rubric:** U7

---

**BUG 12 — Modal only translated on X axis** *(css/style.css, `.modal`)*
- `transform: translateX(-50%)` should be `transform: translate(-50%, -50%)`.
- **Effect:** Modal is horizontally centred but starts below the vertical midpoint, partially off-screen.
- **Fix:** Change to `transform: translate(-50%, -50%)`.
- **File:** `css/style.css`
- **Rubric:** U4

---

**BUG 13 — Sidebar hidden on mobile with no alternative** *(css/style.css, `@media (max-width: 768px)`)*
- `.sidebar { display: none; }` with no hamburger or mobile nav replacement.
- **Effect:** Navigation is completely inaccessible on mobile.
- **Fix:** Provide a mobile nav alternative (hamburger button, bottom nav, etc.).
- **File:** `css/style.css`
- **Rubric:** R1, Bonus B5

---

### ⚙️ Category C — JavaScript Logic Bugs

**BUG 14 — Priority not validated on task creation** *(js/ui.js, `handleAddTask`)*
- Only `title` is validated. If priority is left at the default empty string, the task is created with `priority: ""`, saved, and then silently skipped during render (no matching column).
- **Fix:** Add `if (!priority) { showToast('⚠️ Please select a priority.'); return; }`.
- **File:** `js/ui.js`
- **Rubric:** F3

---

**BUG 15 — Assignment `=` instead of `===` in filter** *(js/ui.js, `renderBoard`)*
- `t.done = true` permanently mutates every task's `done` property to `true` when the "Done" filter is active.
- **Effect:** Switching to the Done filter corrupts all task state — every task becomes permanently "done".
- **Fix:** Change `t.done = true` to `t.done === true`.
- **File:** `js/ui.js`
- **Rubric:** F6, F4, F8

---

**BUG 15b — Active nav state uses `innerHTML` matching** *(js/app.js, `setActiveNav`)*
- The IIFE compares `item.innerHTML.includes(page)` which is fragile and broken — it matches raw HTML string content, not the href.
- **Effect:** Active nav item is never highlighted correctly when navigating between pages.
- **Fix:** Compare `item.getAttribute('href')` to the current page filename.
- **File:** `js/app.js`
- **Rubric:** U-Nav

---

**BUG 16 — Escape key uses deprecated `'Esc'` string** *(js/app.js, `keydown` listener)*
- `e.key === 'Esc'` — modern browsers emit `'Escape'`.
- **Effect:** Pressing Escape never closes the modal.
- **Fix:** Change `'Esc'` to `'Escape'`.
- **File:** `js/app.js`
- **Rubric:** F10

---

**BUG 17 — Delete logic is inverted** *(js/ui.js, `handleCardAction 'delete'`)*
- `tasks.filter(t => t.id === id)` keeps only the clicked task and removes everything else.
- **Fix:** Change to `tasks.filter(t => t.id !== id)`.
- **File:** `js/ui.js`
- **Rubric:** F5

---

**BUG 18 — Completed counter uses wrong condition** *(js/ui.js, `initDashboard`)*
- `tasks.filter(t => !t.done).length` is used for the `done` count — always shows the count of *incomplete* tasks.
- **Fix:** Change to `tasks.filter(t => t.done).length`.
- **File:** `js/ui.js`
- **Rubric:** F8

---

**BUG 19 — localStorage key mismatch between save and load** *(js/app.js)*
- `saveTasks()` writes to `'taskflow_taks'` (typo), but `loadTasks()` reads from `'taskflow_tasks'`.
- **Effect:** Tasks are written to one key and read from another — data never persists across page navigations.
- **Fix:** Make both use the same `STORAGE_KEY` constant: `localStorage.setItem(STORAGE_KEY, ...)` and `localStorage.getItem(STORAGE_KEY)`.
- **File:** `js/app.js`
- **Rubric:** F-Persist

---

**BUG 20 — Inconsistent date formatting** *(js/app.js, `formatDate`)*
- `toLocaleDateString` uses `day: '2-digit'` but `month: 'numeric'` — produces mixed-padding output like `"04/5/2025"`.
- **Fix:** Use `month: '2-digit'` (or `month: 'long'`) consistently.
- **File:** `js/app.js`
- **Rubric:** U8

---

**BUG 9b — Email field uses wrong input type** *(settings.html)*
- Profile email field uses `type="text"` instead of `type="email"`.
- **Effect:** No email format validation on the field.
- **Fix:** Change to `type="email"`.
- **File:** `settings.html`
- **Rubric:** U-Settings / UX

---

## Summary Table

| Bug # | Category | File(s) | Difficulty | Rubric Impact |
|-------|----------|---------|------------|---------------|
| 1  | HTML | All pages | Easy | R1 |
| 2  | HTML | All pages | Easy | F-Nav |
| 3  | HTML | index.html | Medium | F9 |
| 4  | HTML | tasks.html | Medium | U2 |
| 5  | JS   | ui.js | Medium | F-Settings |
| 6  | HTML+JS | tasks.html, ui.js | Easy | F2 |
| 7  | CSS  | style.css | Easy | U3 |
| 8  | CSS  | style.css | Easy | U1 |
| 9  | CSS  | style.css | Easy | U5, R3 |
| 9b | HTML | settings.html | Easy | UX |
| 10 | CSS  | style.css | Easy | U-Polish |
| 10b| CSS  | pages.css | Easy | R1, U6 |
| 11 | CSS  | pages.css | Medium | U-Cards |
| 11b| CSS  | pages.css | Medium | U7 |
| 12 | CSS  | style.css | Easy | U4 |
| 13 | CSS  | style.css | Medium | R1, Bonus |
| 14 | JS   | ui.js | Easy | F3 |
| 15 | JS   | ui.js | Hard | F4, F6, F8 |
| 15b| JS   | app.js | Medium | U-Nav |
| 16 | JS   | app.js | Easy | F10 |
| 17 | JS   | ui.js | Medium | F5 |
| 18 | JS   | ui.js | Medium | F8 |
| 19 | JS   | app.js | Hard | F-Persist |
| 20 | JS   | app.js | Easy | U8 |

---
---

# 📊 Marking Rubric — UI & UX Only (100 Points)

> Judges open each page in a browser and interact with it directly.
> **Do not look at source code.** Resize the window to test responsiveness.
> Test by opening `index.html` locally — no server required.

---

## Section 1 — Navigation & Cross-Page Flow (15 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| All sidebar nav links navigate to the correct page | 6 pts | 2 pts per working link | All broken |
| Active nav item is visually highlighted on each page | 3 pts | 1 pt: highlighted on some pages | Never highlighted |
| Top bar title reflects the current page name | 2 pts | 1 pt: some pages correct | Never correct |
| Topbar action buttons have proper spacing from the right edge | 2 pts | 1 pt: slight clipping | Completely clipped |
| Sidebar task count badge shows correct pending count | 2 pts | 1 pt: shown but incorrect | Not shown |

---

## Section 2 — Functional Correctness (40 pts)

### 2.1 Task Creation — tasks.html (14 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| "+ New Task" button opens the modal | 3 pts | — | Nothing happens |
| Submitting with title + priority adds the card to the correct column | 5 pts | 2 pts: card appears but wrong column | No card appears |
| Validation prevents submission without title OR without priority | 4 pts | 2 pts: one field validated | No validation |
| Modal closes and form resets after submission | 2 pts | 1 pt: closes but doesn't reset | Modal stays open |

### 2.2 Task Actions — tasks.html (12 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| "✔ Done" marks the card as complete (faded, text changes to "Undo") | 4 pts | 2 pts: visual or label works but not both | No effect |
| "Undo" restores the card to active state | 3 pts | 1 pt: partial restore | Broken |
| "🗑 Delete" removes only the clicked task; others remain | 5 pts | 2 pts: deletes but also affects others | Wrong task deleted |

### 2.3 Filter & Search — tasks.html (8 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| "Pending" filter shows only incomplete tasks | 3 pts | 1 pt: partial | No effect |
| "Done" filter shows only completed tasks **without corrupting state** | 3 pts | 1 pt: shows some but corrupts | Broken |
| Search filters tasks in real time | 2 pts | 1 pt: works on submit only | No effect |

### 2.4 Persistence (3 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| Tasks added on tasks.html appear correctly on index.html dashboard after navigating | 3 pts | 1 pt: some tasks persist | Tasks disappear on navigation |

### 2.5 Settings page — settings.html (3 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| Clicking settings nav tabs (Profile, Notifications, etc.) shows the correct panel | 3 pts | 1 pt: some tabs work | No tab switching |

---

## Section 3 — Visual Correctness & Polish (25 pts)

### 3.1 Typography & General (5 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| Page uses a clean sans-serif font (not browser serif default) | 3 pts | — | Serif font used throughout |
| Text hierarchy is clear (headings, labels, body text are distinct) | 2 pts | 1 pt: partial | No hierarchy |

### 3.2 Dashboard (6 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| Four stat cards fit on screen without overflow (desktop) | 3 pts | 1 pt: mostly fits | Obvious overflow |
| Progress bar fill grows proportionally to task completion % | 3 pts | 1 pt: % text correct but bar doesn't fill | Neither works |

### 3.3 Task Board (8 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| Three columns are visually distinct (headers, borders, or backgrounds) | 3 pts | 1 pt: partially separated | Indistinguishable |
| Task cards have a coloured left border matching priority (red/yellow/green) | 3 pts | 1 pt: some colours correct | No priority colour |
| Long task titles are truncated with ellipsis (not overflowing the card) | 2 pts | 1 pt: contained but no ellipsis | Text overflows |

### 3.4 Modal (6 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| Modal is centred both horizontally AND vertically | 4 pts | 2 pts: centred on one axis only | Off-screen |
| Backdrop is visible; clicking it closes the modal | 2 pts | 1 pt: visible but click doesn't close | No backdrop |

---

## Section 4 — Responsiveness (10 pts)

> Test at ~1200px (desktop), ~768px (tablet), ~375px (mobile).

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| No horizontal scrolling on any page at any tested width | 3 pts | 1 pt per width that works | All widths scroll |
| Task board stacks to 1 column on mobile | 2 pts | 1 pt: partial | No change |
| Stat grid shows 2 columns on tablet/mobile | 2 pts | 1 pt: one breakpoint correct | Always 4 columns |
| Controls row (search + filter pills) wraps on small screens | 1 pt | — | Overflows |
| Escape key closes the task modal | 2 pts | — | No effect |

---

## Section 5 — UX Quality (10 pts)

| Criterion | Full | Partial | Zero |
|-----------|------|---------|------|
| Empty column states show a placeholder when a column has no tasks | 2 pts | 1 pt: some columns | Never shown |
| Toast / feedback shown after adding, deleting, or archiving a task | 3 pts | 1 pt per action type | No feedback |
| Hover states on buttons and interactive elements | 3 pts | 1 pt: some hover states | None |
| Overall site feels visually coherent and professional | 2 pts | 1 pt: mostly coherent | Broken layout |

---

## Section 6 — Bonus (up to +15 pts)

| Bonus | Description | Points |
|-------|-------------|--------|
| B1 | Column count badges update dynamically as tasks are added/moved | +3 pts |
| B2 | Overdue task cards visually distinguished (e.g. red due date text) | +3 pts |
| B3 | Smooth CSS animations on card add/remove | +3 pts |
| B4 | Mobile-accessible navigation (sidebar toggle or bottom bar) | +3 pts |
| B5 | Archive page is fully functional (archive from tasks, restore from archive) | +3 pts |

---

## Final Score Summary

| Section | Max |
|---------|-----|
| 1 — Navigation & Cross-Page Flow | 15 |
| 2 — Functional Correctness | 40 |
| 3 — Visual Correctness & Polish | 25 |
| 4 — Responsiveness | 10 |
| 5 — UX Quality | 10 |
| **Core Total** | **100** |
| 6 — Bonus | +15 |

---

## Judge's Checklist

1. Open `index.html` in Chrome or Firefox (no server needed — file:// works).
2. Add 4–6 tasks with a mix of priorities via the Tasks page before scoring.
3. Mark 2 tasks as done; check stats on Dashboard.
4. Navigate between all 4 pages and check nav links work.
5. Resize to 768px and 375px for responsiveness checks.
6. Press Escape while modal is open.
7. Click "Done" filter on Tasks page — then check if other tasks are still intact.
8. Try to delete one task — confirm only that task disappears.
9. Reload the page — check if tasks persist.
