# TaskFlow

A lightweight, single-page task management application with a clean, modern interface. Built with vanilla HTML, CSS, and JavaScript.

## Features

- **Task Management** - Create, edit, delete, and complete tasks
- **Priority Levels** - Low (0), Medium (1), and High (2) with color-coded badges
- **Status Tracking** - Pending, In Progress, and Done
- **Due Dates** - Visual countdown with color-coded urgency indicators
- **Tags** - Add up to 8 custom tags per task
- **Statistics Dashboard** - Quick overview of Total, Pending, and Done tasks
- **Accessibility** - ARIA labels, keyboard support (Escape to close), focus management
- **Data-testid attributes** - Ready for automated testing

## Getting Started

Simply open `index.html` in any modern web browser.

```bash
# Using Python's built-in server
python3 -m http.server 8000

# Using Node.js
npx serve

# Using PHP
php -S localhost:8000
```

Then navigate to `http://localhost:8000`

## Usage

### Create a Task
1. Click the **New Task** button
2. Fill in the required fields (title, priority, due date)
3. Optionally add description, status, and tags
4. Click **Add Task**

### Edit a Task
1. Click the **Edit** button on any task card
2. Modify the details in the modal form
3. Click **Save Changes**

### Delete a Task
1. Click the **Delete** button on any task card

### Complete a Task
- Toggle the checkbox on any task to mark it complete/incomplete

### Keyboard Shortcuts
- **Escape** - Close the modal

## Color Guide

### Priority Colors
| Priority | Badge Class | Color |
|----------|-------------|-------|
| High (2) | badge-high | Red (#993C1D on #FAECE7) |
| Medium (1) | badge-medium | Orange (#854F0B on #FAEEDA) |
| Low (0) | badge-low | Green (#085041 on #E1F5EE) |

### Due Date Indicators
| Time Remaining | Badge Class | Color |
|----------------|-------------|-------|
| Overdue | tr-overdue | Red (#A32D2D on #FCEBEB) |
| Due today/within 24h | tr-today | Orange (#993C1D on #FAECE7) |
| Tomorrow - 5 days | tr-soon | Yellow (#854F0B on #FAEEDA) |
| 6+ days | tr-future | Green (#0F6E56 on #E1F5EE) |

## Project Structure

```
Task-Flow/
├── index.html    # Main application file (contains all HTML, CSS, and JS)
├── README.md     # Project documentation
└── .git/         # Git repository
```

## Technical Details

- **Architecture**: Single-file application (all code embedded in index.html)
- **State Management**: In-memory JavaScript array with global variables
- **Data Persistence**: None (data resets on page reload)
- **Task Data Model**:
  ```javascript
  {
    id: number,
    title: string,
    desc: string,
    priority: 0 | 1 | 2,
    status: "Pending" | "In Progress" | "Done",
    due: Date,
    tags: string[],
    done: boolean
  }
  ```

## Browser Support

- Chrome/Edge 88+
- Firefox 85+
- Safari 14+

## Decisions Made

### Single-file architecture
Everything lives in one index.html. No framework, no bundler, no Node. This keeps the project zero-dependency and instantly runnable by anyone — just open the file. For a component-scale task like this, a React or Vue setup would have been over-engineering.

### Vanilla JS over a framework
The task spec called for testability and semantic HTML correctness, not component reactivity. Vanilla JS gave full control over the DOM and data-testid attributes without any abstraction layer interfering with the automated tests.

### Modal-driven add/edit flow
Rather than inline editing or separate pages, a modal form was chosen for both adding and editing tasks. This keeps the card list clean and readable while giving users a focused, distraction-free space to fill in all required fields. It also mirrors patterns used in real-world tools like Asana and Linear.

### Teal + white colour palette
Teal (#1D9E75, #0F6E56) was chosen as the primary accent against white cards and a deep teal background (#0a2e2b). This gives strong contrast, passes WCAG AA, and creates a calm but focused productivity feel — deliberately distinct from the generic purple/blue AI aesthetic.

### Real `<input type="checkbox">`
The spec explicitly required either a real checkbox or a role="checkbox" button. A native `<input type="checkbox">` was used because it comes with built-in keyboard support (Space to toggle), focus management, and screen reader announcements for free — no JavaScript needed for those behaviours.

### `<time>` element with datetime attribute
Both the due date and time remaining use the `<time>` element with a machine-readable datetime attribute. This improves SEO and screen reader output — assistive tech can announce dates in the user's preferred locale format.

### Tag system
Tags are stored as plain string arrays per task. Users can add tags via the modal input and remove them by clicking. Each rendered tag maps to a `<li>` inside a `<ul role="list">` for correct semantics, with data-testid attributes on work and urgent tags as required.

### Live time remaining
Calculated from Date.now() vs the task's due date on every render, plus a setInterval refresh every 60 seconds. The output element is wrapped in aria-live="polite" so screen readers announce updates without interrupting the user.

### Header stats bar
Total, Pending, and Done counts are derived directly from the task array on every render — no separate state to keep in sync. Simple and reliable.

## Trade-offs

| Decision | Trade-off |
|----------|-----------|
| Single HTML file | Easy to run and share, but doesn't scale to a multi-page app. Would be split into components in a real codebase. |
| No localStorage | Tasks reset on page refresh. Kept out deliberately to avoid scope creep in Stage 0 — straightforward to add later. |
| No backend | All data is in-memory JS arrays. A real app would hit an API. |
| Inline JS event handlers (onclick="...") | Slightly less clean than addEventListener but keeps the code readable without module scope issues in a single-file setup. |
| CSS in a `<style>` block | Works fine for one file. In production this would be a separate stylesheet or CSS modules. |
| No drag-to-reorder | Intentionally deferred — adds complexity and wasn't in the Stage 0 requirements. |

## Accessibility Checklist

- All data-testid attributes present and correctly named
- Real `<input type="checkbox">` with linked `<label>` and aria-label
- All buttons have accessible names (visible text + aria-label)
- Priority and status badges have aria-label
- Time remaining wrapped in aria-live="polite"
- Semantic HTML: `<article>`, `<h2>`, `<p>`, `<time>`, `<ul role="list">`, `<button>`
- Visible focus styles on all interactive elements
- Fully keyboard navigable (Tab → checkbox → Edit → Delete)
- WCAG AA colour contrast on all text

## License

MIT
