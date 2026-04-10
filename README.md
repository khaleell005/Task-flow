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

## License

MIT
