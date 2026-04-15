# TaskFlow

A lightweight, single-page task management application with a clean, modern interface. Built with vanilla HTML, CSS, and JavaScript.

**Stage 1** - Enhanced interactive Todo Card with inline editing, status transitions, priority indicators, and expand/collapse behavior.

## Features

- **Task Management** - Create, edit, delete, and complete tasks
- **Inline Edit Mode** - Edit tasks directly on the card with a form overlay
- **Priority Levels** - Low (0), Medium (1), and High (2) with color-coded badges and visual indicators
- **Status Transitions** - Pending, In Progress, and Done with dropdown control
- **Due Dates** - Granular countdown with color-coded urgency indicators
- **Expand/Collapse** - Long descriptions can be collapsed with a toggle
- **Overdue Indicators** - Explicit visual badge when tasks are overdue
- **Tags** - Add up to 8 custom tags per task
- **Statistics Dashboard** - Quick overview of Total, Pending, and Done tasks
- **Accessibility** - ARIA labels, keyboard support, focus management
- **Data-testid attributes** - Ready for automated testing (Stage 0 + Stage 1 testids)

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

### Edit a Task (Inline)
1. Click the **Edit** button on any task card
2. The inline edit form appears below the task
3. Modify title, description, priority, or due date
4. Click **Save Changes** or **Cancel**

### Status Transitions
- Use the **status dropdown** below the task to change status
- Toggling the **checkbox** automatically sets status to "Done"
- Setting status to "Done" automatically checks the checkbox
- Unchecking checkbox reverts status to "Pending"

### Complete a Task
- Toggle the checkbox on any task to mark it complete/incomplete
- When complete, the task shows muted styling with strikethrough

### Expand/Collapse Description
- Long descriptions (>120 characters) are collapsed by default
- Click **"Show more"** to expand and **"Show less"** to collapse
- Toggle is keyboard accessible

### Keyboard Shortcuts
- **Escape** - Close the modal
- **Tab** - Navigate between form fields
- **Space/Enter** - Activate buttons and toggles

## Data-testid Attributes

### Stage 0 Testids (Preserved)
| Element | testid |
|---------|--------|
| Task card | `test-todo-card` |
| Checkbox toggle | `test-todo-complete-toggle` |
| Task title | `test-todo-title` |
| Description | `test-todo-description` |
| Priority badge | `test-todo-priority` |
| Status badge | `test-todo-status` |
| Due date | `test-todo-due-date` |
| Time remaining | `test-todo-time-remaining` |
| Tags list | `test-todo-tags` |
| Edit button | `test-todo-edit-button` |
| Delete button | `test-todo-delete-button` |

### Stage 1 Testids (New)
| Element | testid |
|---------|--------|
| Edit form container | `test-todo-edit-form` |
| Title input | `test-todo-edit-title-input` |
| Description textarea | `test-todo-edit-description-input` |
| Priority select | `test-todo-edit-priority-select` |
| Due date input | `test-todo-edit-due-date-input` |
| Save button | `test-todo-save-button` |
| Cancel button | `test-todo-cancel-button` |
| Status control | `test-todo-status-control` |
| Priority indicator | `test-todo-priority-indicator` |
| Expand toggle | `test-todo-expand-toggle` |
| Collapsible section | `test-todo-collapsible-section` |
| Overdue indicator | `test-todo-overdue-indicator` |

## Color Guide

### Priority Colors
| Priority | Badge | Indicator Dot | Border Accent |
|----------|-------|--------------|---------------|
| High (2) | Red (#993C1D) | Red dot | Red left border |
| Medium (1) | Orange (#854F0B) | Orange dot | - |
| Low (0) | Green (#085041) | Green dot | - |

### Due Date Indicators
| Time Remaining | Badge Class | Color |
|----------------|-------------|-------|
| Overdue | tr-overdue | Red (#A32D2D on #FCEBEB) |
| Due now - 1 hour | tr-today | Orange |
| 1-24 hours | tr-today | Orange |
| Tomorrow - 5 days | tr-soon | Yellow |
| 6+ days | tr-future | Green |
| Completed | tr-completed | Gray |

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
- **Time Updates**: Every 30 seconds via setInterval
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
    done: boolean,
    expanded: boolean
  }
  ```

## Browser Support

- Chrome/Edge 88+
- Firefox 85+
- Safari 14+

## What's New in Stage 1

### Inline Edit Mode
Replaced modal-only editing with inline form editing directly on the task card. The edit form includes all required fields with proper testids.

### Status Transitions
Added a status dropdown control that:
- Syncs bidirectionally with the checkbox
- Allows explicit status changes without toggling completion
- Updates all visual indicators immediately

### Priority Visual Indicators
Added multiple visual indicators for priority:
- Color-coded badge
- Priority dot next to the badge
- Left border accent on high-priority cards

### Expand/Collapse Behavior
Descriptions over 120 characters are collapsed by default with a "Show more/less" toggle button that is keyboard accessible.

### Enhanced Time Handling
- Granular time display (minutes, hours, days)
- Explicit "Overdue" badge when past due
- Time stops updating for completed tasks
- Updates every 30 seconds

### Visual State Changes
| State | Visual Treatment |
|-------|-----------------|
| Done | Strikethrough title, muted colors, reduced opacity |
| High Priority | Red dot, red border accent |
| Overdue | Red border, "Overdue" badge |
| In Progress | Standard styling with status badge |

## Design Decisions

### Inline vs Modal Editing
Stage 1 uses inline editing on the card rather than only modal editing. This allows quick edits without leaving context of the task list. Modal editing is still available for complex edits via the New Task button.

### Segmented vs Dropdown Status Control
A dropdown select was chosen over segmented buttons because:
- More room on the card for other content
- Easier to add more statuses later
- Native select is keyboard accessible out of the box

### Expand/Collapse Threshold
120 characters was chosen as the collapse threshold. This keeps short descriptions readable while preventing very long task descriptions from dominating the card list.

### Time Update Interval
30 seconds was chosen for Stage 1 (reduced from 60 seconds in Stage 0) to provide more responsive time updates without excessive DOM updates.

## Known Limitations

- No localStorage persistence
- No drag-to-reorder
- No keyboard focus trap in edit form
- Modal and inline edit both exist (potential for UX confusion)

## Accessibility Checklist

- All Stage 0 testids preserved
- All Stage 1 testids added with correct naming
- Real `<input type="checkbox">` with linked `<label>` and aria-label
- All buttons have accessible names
- Priority and status badges have aria-label
- Priority indicator has aria-hidden and title for context
- Time remaining wrapped in aria-live="polite"
- Overdue indicator announced with aria-label
- Expand toggle has aria-expanded and aria-controls
- Status control has proper label association
- Inline form has role="form" and aria-label
- Visible focus styles on all interactive elements
- Fully keyboard navigable
- WCAG AA colour contrast on all text

## License

MIT
