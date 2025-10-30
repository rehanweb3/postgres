# PostgreSQL Client Design Guidelines

## Design Approach

**Selected Approach:** Design System - Drawing from professional database tools and code editors

**Primary References:**
- TablePlus/DataGrip for database client UX patterns
- VS Code for editor integration and panel management
- Linear for clean, modern professional aesthetics
- Fluent Design for data-heavy interfaces

**Core Principle:** Prioritize efficiency, clarity, and professional polish. Every pixel serves the user's workflow.

---

## Layout System

### Application Structure
**Three-Panel Layout:**
- **Left Sidebar (280px fixed):** Connection management, schema tree navigation
- **Center Panel (flexible, min 400px):** Primary content area - table viewer, query results, data grid
- **Right Panel (320px, collapsible):** Properties inspector, query history, connection details

**Spacing Primitives:**
Use Tailwind units: **2, 3, 4, 6, 8** for consistent spacing
- Component padding: `p-4` to `p-6`
- Section spacing: `gap-4` for grids, `space-y-6` for vertical stacks
- Panel padding: `p-6` to `p-8`
- Tight elements (pills, tags): `px-2 py-1`

### Responsive Behavior
- Desktop (1280px+): Full three-panel layout
- Tablet (768-1279px): Collapsible sidebar, two-panel view
- Mobile (< 768px): Single panel with drawer navigation

---

## Typography System

**Font Stack:**
- **Primary:** Inter (via Google Fonts) - UI elements, labels, buttons
- **Code/Monospace:** JetBrains Mono (via Google Fonts) - SQL editor, data values, connection strings

**Hierarchy:**
- **Page Titles:** text-2xl (24px), font-semibold
- **Section Headers:** text-lg (18px), font-semibold
- **Panel Headers:** text-base (16px), font-medium
- **Body/Labels:** text-sm (14px), font-normal
- **Data Grid Text:** text-sm (14px), font-mono
- **Helper Text:** text-xs (12px)
- **SQL Editor:** text-sm (14px), font-mono, leading-relaxed

**Line Heights:**
- Headers: leading-tight
- Body: leading-normal
- Code/Data: leading-relaxed for better readability

---

## Component Library

### Navigation & Sidebar

**Connection Panel:**
- Accordion-style connection list with expand/collapse
- Two-mode toggle: "Connection String" / "Manual Entry"
- Form layout: Single column, full-width inputs with consistent `space-y-4`
- SSL toggle with conditional certificate upload section
- Connect button: Full width, prominent placement

**Schema Tree:**
- Hierarchical tree structure: Database → Tables → Columns
- Expandable nodes with chevron indicators
- Icon system: Table icon, column type icons (string, number, date)
- Selected state highlighting for active table/column
- Virtualized rendering for large schemas

### Data Display

**Table Data Grid:**
- Fixed header row with column names, types, and constraints
- Zebra striping for row alternation (subtle)
- Hover state on rows
- Cell padding: `px-3 py-2`
- Inline editing: Double-click to edit, escape to cancel
- Pagination controls at bottom: `<< < 1 2 3 > >>`
- Row selection checkboxes for bulk operations

**Schema Information Panel:**
- Card-based layout with sections: Columns, Indexes, Constraints
- Definition list pattern: Label (semibold) + Value pairs
- Monospace for technical values (data types, constraints)

### SQL Editor

**Editor Component (Monaco/CodeMirror):**
- Full-height panel with minimum 300px
- Syntax highlighting for PostgreSQL
- Line numbers on left
- Execution controls above editor: Run Query, Clear, Format
- Query validation indicator (live feedback)
- Result pane below with toggle: Table View / JSON View

**Query Results:**
- Same grid component as table viewer
- Execution stats: Rows affected, execution time
- Error messages: Dedicated error banner with icon and message

### Forms & Inputs

**Input Fields:**
- Label above input: text-sm font-medium mb-2
- Input height: h-10, padding: px-3
- Border: 1px solid (neutral)
- Focus state: ring-2 outline pattern
- Helper text below: text-xs, space-y-1

**File Upload (SSL Certificates):**
- Drag-and-drop zone with border-dashed
- File name display after selection
- Clear file button (× icon)
- Upload area height: h-32

**Buttons:**
- Primary: Full-width in forms, inline in toolbars
- Height: h-10 for standard, h-8 for compact
- Padding: px-4 for standard, px-3 for compact
- Icon + text pattern where appropriate

### Status & Feedback

**Connection Status Indicator:**
- Pill badge in top-right: Connected (green dot) / Disconnected (gray dot)
- Connection name + database name display
- Disconnect action available when connected

**Notifications:**
- Toast system for success/error messages
- Position: top-right, fixed
- Auto-dismiss after 4 seconds
- Error messages: Persist until dismissed

### Panels & Cards

**Panel Pattern:**
- Border on all sides
- Header section with title and actions
- Content area with appropriate padding
- Resizable panels with drag handle

**Card Component:**
- Used for connection entries, table previews
- Padding: p-4
- Hover state with subtle elevation change
- Click target for navigation

---

## Interaction Patterns

### Navigation Flow
1. Connection form → Schema viewer → Table selection → Data grid/SQL editor
2. Breadcrumb trail showing: Connection > Database > Table
3. Quick switch between tables via sidebar without losing query

### Data Manipulation
- **View Mode:** Read-only data grid
- **Edit Mode:** Click "Edit" button → Inline cell editing enabled
- **SQL Mode:** Write queries directly in editor
- **Validation:** Real-time feedback on dangerous queries (visual warning before execution)

### Multi-Panel Management
- Resizable panel dividers (4px wide, visible on hover)
- Panel collapse/expand icons in panel headers
- Remember panel sizes in session storage

---

## Spacing & Layout Specifications

**Container Hierarchy:**
- App wrapper: Full viewport (h-screen w-screen)
- Header bar: h-14 with px-6
- Main content area: flex-1 with overflow handling
- Sidebar: px-4 py-6
- Content panels: p-6 to p-8

**Grid Systems:**
- Form grid: Single column, max-w-md
- Data grid: Dynamic columns with min-width constraints
- Schema tree: Indentation: pl-4 per level

**Whitespace Strategy:**
- Dense information areas: gap-2 to gap-3
- Form sections: space-y-6
- Panel sections: space-y-4
- Related elements: gap-2

---

## Accessibility Standards

- All interactive elements: Minimum 44x44px touch target
- Keyboard navigation: Full support for all actions
- Focus indicators: Visible 2px ring on all focusable elements
- ARIA labels: Descriptive labels for icons and actions
- Screen reader support: Proper heading hierarchy, landmark regions
- Color contrast: Minimum WCAG AA compliance

---

## Professional Polish Details

- **Micro-interactions:** Subtle transitions (150ms) on hover states
- **Loading States:** Skeleton screens for data grids, spinner for queries
- **Empty States:** Helpful messages with next-step guidance
- **Keyboard Shortcuts:** Display shortcuts in tooltips (e.g., "Cmd+Enter to run")
- **Context Menus:** Right-click on tables/columns for quick actions
- **Drag Handles:** Visual feedback on resizable panels

This design creates a professional, efficient database client that feels modern, powerful, and purpose-built for developers working with PostgreSQL databases.