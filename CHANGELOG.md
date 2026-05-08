# Changelog

All notable changes to the Velocity Implementations Dashboard are documented here.

---

## [1.2.0] — May 8, 2026

### New Features

#### Core Platform & Provider Fields
- Added **Current Core Platform** column to Projects table, detail modal, Risk Flags, Stale Projects, Tasks, and all exports
- Added **Current Core Provider Company Name** support throughout the dashboard
- **Core Platform Distribution** chart on the Overview tab is now a collapsible two-level tree grouped by Provider Company → Platform; defaults to collapsed (provider totals only), click any provider to expand its platforms
- **Core Platforms** pill section added to each Resource scorecard showing provider breakdown for that engineer's assigned projects
- Core Platform filter added to the Projects tab filter bar

#### Projects by Type — Three New Default Types
- **Migration** (keyword: `Migration`) — Red badge
- **Acquisition** (keyword: `Acquisition`) — Red badge
- **Core Conversion** (keyword: `Conversion`) — Red badge

---

## [1.1.0] — April 30, 2026

### New Features

#### Data Loading
- Two-file upload flow on dashboard launch (Projects export + Tasks/FY27 extract)
- All parsing runs locally in the browser — no data leaves the machine
- Embedded April 30, 2026 snapshot for offline / demo use
- **Refresh Data** button in header to reload fresh exports without closing the browser
- Robertson, Donita automatically excluded from all data and calculations (dummy template PM)

#### Tabs
- **Tasks tab** — full open-task listing grouped by Resource → Customer, sorted oldest due date first; collapsible with Collapse All / Expand All; 9 filters including Critical and Past Due toggles
- **Stale Projects tab** — all projects with no status update in 30+ days, separated from Risk Flags into its own tab with Type and PM filters
- **Insights tab** — instant computed portfolio analysis (no API required); health score, six analysis cards, and prioritized recommended actions

#### Projects Tab
- Two-level collapsible grouping: **PM → Customer Number**; defaults to fully collapsed
- PM header rows show active count and at-risk pill summary
- Customer number pill, company name, and project count in sub-headers
- **Collapse All / Expand All** button
- Project Type column and filter
- Core Platform column and filter

#### Tasks Tab
- Two-level collapsible grouping: **Resource → Customer Number**; defaults to fully collapsed
- Oldest-due-date-first sort within each customer group
- Past due count and critical count shown in group headers
- 9 simultaneous filters: Search, Customer #, Type, PM, Status, Schedule, Resource, Core Platform, Critical, Past Due

#### Resources Tab
- Three clickable metric tiles per engineer: **Due in 14 Days**, **Critical — 7 Days**, **Overdue Tasks**
- Clicking a tile navigates to the Tasks tab with resource and date filters pre-applied
- **Project Types** pill section per resource card
- **Core Platforms** pill section per resource card

#### Risk Flags Tab
- **Status Updated** column with color-coded dates (green <15d, amber 15–29d, red 30+d)
- Core Platform column

#### Overview Tab
- **Core Platform Distribution** bar chart (upgraded to collapsible tree in v1.2)
- Projects by Type card expanded with full status breakdown per type

#### Configuration Tab
- Moved to far right of tab bar
- Full Project Type rule editor: label, keywords, badge color, priority order (↑↓)
- Add / Remove / Reset to Defaults
- Changes propagate instantly across all tabs, filters, exports, and Insights

#### Exports
- Export buttons on Projects, Tasks, Risk Flags, and Stale Projects tabs
- All exports respect active filters
- Date-stamped filenames: `Velocity_Projects_YYYY-MM-DD.xlsx`, etc.
- Core Platform column included in all exports

---

## [1.0.0] — Initial Release

- Portfolio overview with KPI tiles, status donut, schedule health grid
- Projects table with PM, Status, Schedule, Progress, Finish Date, Open Tasks, Resources columns
- Timeline / Gantt view with Today marker
- Resources tab with effort completion bars
- Risk Flags tab
- Project Type classification engine with 7 default rules
- Detail modal for each project
