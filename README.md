# Velocity Implementations Dashboard
**Version 1.2 · FY27 Project Portfolio · May 2026**

A fully self-contained HTML dashboard for managing and analyzing Velocity's implementation project portfolio. All data processing happens locally in the browser — no data is ever uploaded to a server.

---

## Getting Started

Open the dashboard HTML file in any modern browser. On launch you will see a load screen prompting you to upload two Excel exports from Dynamics:

1. **Projects File** — Velocity Dashboard Projects export
2. **Tasks File** — FY27 Project Extract (task & resource data)

Once both files are selected, click **Load Dashboard**. Alternatively, click *Continue with embedded snapshot data* to open immediately using the April 30, 2026 snapshot baked into the file.

A **Refresh Data** button in the top-right header allows you to reload fresh exports at any time without closing the browser.

---

## Tabs

### Overview
High-level portfolio health at a glance.

- **KPI tiles** — Total projects, In-Progress, Not Started, On-Hold, Live/Wrapping, At Risk/Delayed
- **Portfolio Status Breakdown** — Donut chart of all project statuses
- **Schedule Health** — Grid of schedule flag categories with counts
- **Projects by PM** — Horizontal bar chart of project counts per Project Manager
- **Core Platform Distribution** — Collapsible two-level bar chart grouped by Core Provider Company, expanding to individual Core Platform counts. Defaults to collapsed (provider level only); click any provider row to reveal its platforms
- **Top Incomplete Task Counts** — Bar chart of the 10 projects with the highest open task counts, labeled by project name
- **Projects by Type** — Tile grid showing per-type breakdowns (active, on-hold, live, delayed, avg % complete)

---

### Projects
Full project listing with two-level collapsible grouping.

**Grouping hierarchy:**
- **Level 1 — PM** (navy header) — shows project count, customer count, active count, and at-risk pill
- **Level 2 — Customer Number** (gray sub-header) — shows 4-digit customer number, company name, project count
- **Level 3 — Project rows** — indented, sorted by customer number

Defaults to fully collapsed (PM level only). Use **Collapse All / Expand All** to toggle all groups, or click individual headers to drill in.

**Filters:** Search, PM, Type, Status, Schedule, Core Platform
**Columns:** Project, PM, Type, Status, Schedule, Core Platform, Progress, Finish Date, Open Tasks, Resources
**Clicking any row** opens a detail modal showing all project fields including Core Platform, task effort data, assigned resources, and latest comments.
**Export** button downloads the current filtered view to Excel.

---

### Timeline
Gantt-style chart of project start/finish dates.

- Color-coded bars by project status
- Red "Today" marker showing current date position
- Progress fill within each bar showing % complete
- Project type shown in the row subtitle
- **Filters:** PM, Type, Status
- Click any row to open the project detail modal

---

### Resources
Engineer scorecard view. One card per resource showing:

- **Stats row** — Total tasks, Effort (hrs), Done (hrs)
- **Three clickable metric tiles:**
  - **Due in 14 Days** — tasks finishing within two weeks (amber/red when elevated)
  - **Critical — 7 Days** — critical-flagged tasks due this week (red when >0)
  - **Overdue Tasks** — past-due incomplete tasks (red when >0)
  - Clicking any tile navigates to the Tasks tab with resource and date filters pre-applied
- **Project Types** — pill tags showing type breakdown (ILS × 4, CashPlease × 2, etc.)
- **Core Platforms** — pill tags showing Core Provider Company breakdown for this resource's projects
- **Effort Completion bar** — visual of hours done vs. planned

Below the cards, an **Effort Hours** stacked bar chart compares planned vs. completed hours across all engineers.

---

### Tasks
All open tasks (< 100% complete) with two-level collapsible grouping.

**Grouping hierarchy:**
- **Level 1 — Resource** (navy header) — shows task count, customer count, past due count, critical count
- **Level 2 — Customer Number** (gray sub-header) — shows customer number, company, task count, past due count
- **Level 3 — Task rows** — sorted oldest due date → newest within each group

Defaults to fully collapsed. Use **Collapse All / Expand All** to toggle.

**Filters:** Search, Customer Number, Type, PM, Status, Schedule, Resource, Core Platform, Priority (Critical / Non-Critical), Past Due (All / Past Due Only / Upcoming Only)

**Columns:** Task, Project, Resource, Due Date (red + ⚠ if overdue), Priority, Effort (hrs), % Done, Type, PM, Core Platform, Proj Status

Status bar shows: total tasks · past due count · critical count for the current filter state.
**Export** button downloads the current filtered view to Excel.

---

### Risk Flags
Two sections focused on projects needing management attention.

**At-Risk & Attention Projects** — projects with schedule health flags (Schedule Risk, Needs Attention, Potential Issues), delay statuses, or On-Hold. Sorted by risk score (highest severity first).

**Filters:** Type, PM (apply to both tables)

**Columns:** Project, Type, PM, Status, Schedule, Open Tasks, Finish Date, Status Updated (color-coded: green <15d, amber 15-29d, red 30+d), Core Platform, Notes

**Export** button downloads the at-risk project list to Excel.

---

### Stale Projects
All projects (across all statuses) where Status Updated On is more than 30 days ago, sorted most-stale first.

**Filters:** Type, PM
**Columns:** Project, Type, PM, Status, Schedule, Open Tasks, Finish Date, Status Updated, Core Platform, Days Since Update (red pill showing exact day count)
**Export** button downloads the stale project list to Excel.

---

### Insights
Automatically computed portfolio analysis — no API call or internet connection required. Runs instantly from live dashboard data.

**Health Score banner** — 0–100 computed score weighted across risk %, stale %, delay %, and hold %, plus five KPI tiles (Portfolio Health, Active Projects, At Risk, Stale 30d+, Overdue Tasks).

**Six analysis cards:**
- Portfolio Status Breakdown
- Schedule & Risk Flags
- Stale Status Updates
- Resource Workload
- PM Portfolio Summary
- Core Platform Distribution

**Recommended Actions** — dynamically generated, prioritized High / Medium / Low, naming specific projects, PMs, and engineers based on actual data thresholds.

**Refresh Analysis** button re-runs everything after loading new data.

---

### ⚙ Configuration
User-editable Project Type classification rules. Changes apply instantly across all tabs.

Each rule defines:
- **Label** — the type name displayed in badges and filters (e.g. "ILS", "CashPlease")
- **Keywords** — comma-separated terms matched case-insensitively against the project name. Short tokens (≤3 chars) use word-boundary matching to prevent false positives
- **Badge color** — Blue, Teal, Purple, Orange, Yellow, Green, Red, or Gray

Rules are checked top-to-bottom — first match wins. Use ↑↓ buttons to reorder priority.

**Add Rule** — adds a new blank rule at the bottom.
**Reset to Defaults** — restores the original seven rules plus the three new defaults.

---

## Default Project Type Rules

| Type | Keywords | Badge |
|------|----------|-------|
| CashPlease | CashPlease, CP | Blue |
| ILS | ILS, Intelligent Limit System | Teal |
| ICS | ICS, Invitation Checking System | Purple |
| Account Engagement | AE, Account Engagement | Orange |
| Reg E | REMS, Reg E Management System | Yellow |
| ARS | ARS, Account Revenue | Green |
| MRPC | MRPC, My Rewards Premium Card | Gray |
| Migration | Migration | Red |
| Acquisition | Acquisition | Red |
| Core Conversion | Conversion | Red |

---

## Data Exclusions

The following PMs are automatically excluded from all data and calculations on load:

- **Robertson, Donita** — dummy project template, not a real implementation

To add additional exclusions, edit the `EXCLUDED_PMS` array near the top of the script section.

---

## Data Fields Used

### Projects Export (Dynamics)
| Field | Used For |
|-------|----------|
| Project Number | Join key |
| Name | Display, customer number extraction, type classification |
| Project manager | Grouping, filters, PM analysis |
| Overall Project Status | Status badges, KPIs, risk flags |
| Project Schedule Status | Schedule health, risk flags |
| Start Date / Finish Date | Timeline, overdue detection |
| % Complete | Progress bars |
| Status Updated On | Stale detection (30-day threshold) |
| # of Incomplete Tasks | Open task counts |
| Company Profile | Customer name display |
| Comments | Project detail modal, risk flag notes |
| Current Core Platform | Platform column, filter, distribution chart |
| Current Core Provider Company Name | Provider grouping in distribution chart, resource cards |

### Tasks Export (FY27 Project Extract)
| Field | Used For |
|-------|----------|
| Project Number | Join key to projects |
| Task | Task name |
| Bookable Resource | Engineer assignment, resource tab |
| Start Date / Finish Date | Due date display, overdue detection |
| Effort / Effort Completed / Effort Remaining | Resource workload hours |
| % Complete | Task completion, open task filtering |
| Critical | Critical task flags, resource metrics |

---

## Export File Naming
All exports are date-stamped at time of download:

- `Velocity_Projects_YYYY-MM-DD.xlsx`
- `Velocity_Tasks_YYYY-MM-DD.xlsx`
- `Velocity_RiskFlags_YYYY-MM-DD.xlsx`
- `Velocity_StaleProjects_YYYY-MM-DD.xlsx`
