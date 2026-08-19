# Azure Boards — Agile Project Management (Full Tutorial)

> Comprehensive study notes based on **Day 2** of the *Azure DevOps Zero to Hero* series by *Tech Tutorials with Piyush*. Written so you can understand and revise everything covered without re-watching the video.

---

## Table of Contents

1. [Overview](#overview)
2. [What Are Azure Boards?](#1-what-are-azure-boards)
3. [Work Items](#2-work-items)
4. [Board Processes: Basic, Agile, Scrum, CMMI](#3-board-processes-basic-agile-scrum-cmmi)
5. [The Basic Process Hierarchy (Epic → Issue → Task)](#4-the-basic-process-hierarchy-epic--issue--task)
6. [Hands-On: Creating a Basic Project & Board](#5-hands-on-creating-a-basic-project--board)
7. [Anatomy of a Work Item (Fields Explained)](#6-anatomy-of-a-work-item-fields-explained)
8. [Sprints / Iterations](#7-sprints--iterations)
9. [Hands-On: The Scrum Process (with Demo Data)](#8-hands-on-the-scrum-process-with-demo-data)
10. [Teams, Area Paths & Iteration Paths](#9-teams-area-paths--iteration-paths)
11. [Sprint Planning & Capacity](#10-sprint-planning--capacity)
12. [Customizing the Board (Cards, Columns, Swimlanes)](#11-customizing-the-board-cards-columns-swimlanes)
13. [Dashboards & Widgets](#12-dashboards--widgets)
14. [Queries & Charts](#13-queries--charts)
15. [Customizing the Process (Inherited Processes)](#14-customizing-the-process-inherited-processes)
16. [Quick Revision](#quick-revision)

---

## Overview

**What this covers:** How to use **Azure Boards** — the Agile project-management service inside Azure DevOps — to plan, track, and manage work. It walks through work items, board processes, sprints, capacity planning, board customization, dashboards, queries, and process customization, using both a **Basic** project and a richer **Scrum** project (populated with demo data).

**What you will learn:**

- What Azure Boards is and how it compares to Jira/Notion.
- **Work items** and their types across processes.
- The four **process templates** (Basic, Agile, Scrum, CMMI) and how their complexity differs.
- How to create epics, issues/features, PBIs, and tasks, and link them into a hierarchy.
- **Sprints/iterations**, **capacity planning**, and **story points / remaining work**.
- **Kanban board** customization: styling rules, columns, WIP limits, swimlanes, tags.
- **Dashboards, widgets, queries, and charts**.
- **Inherited processes** to add custom fields.

**Prerequisites:** Day 1 concepts (DevOps, Agile, an Azure DevOps organization and project). Familiarity with Jira/Notion/Kanban helps but isn't required.

> **Additional Context:** *Azure Boards* is one of five core Azure DevOps services (Boards, Repos, Pipelines, Test Plans, Artifacts). This lesson focuses entirely on **Boards**.

---

## 1. What Are Azure Boards?

### Definition

**Azure Boards** is a **project-management tool** used to track a project's progress — what's being worked on, who owns each task, delays, blockers, and improvements for future releases. It is comparable to **Jira** or **Notion**, with advanced features. At its simplest, think of it as an **advanced to-do list**: create items, assign them, track them, and mark them **done**.

### Why It Matters

It gives a team a single, shared, visual place to plan and measure work, replacing scattered spreadsheets and manual tracking. It directly supports the **Agile** way of working introduced in Day 1.

### Important Points

- It is the **Agile planning/tracking** layer of Azure DevOps.
- Core building block = the **work item** (see next section).
- Provides **Kanban boards, backlogs, sprints, dashboards, queries, and charts**.

---

## 2. Work Items

### Definition

A **work item** is the unit through which you **track a single activity** in a project. It can represent many things depending on the process: a **bug, task, feature, issue, epic, user story**, and more.

### How It Works

Each work item lets you measure and manage an activity:

- How long it took / whether there's a **delay** or **blocker**.
- Who is **accountable** (each item is **assigned to a person** responsible for completing it).
- Its current **state** (e.g., To Do → Doing → Done).

> **Key Takeaway:** A work item is the smallest trackable, assignable "thing to do." Good practice is to make the lowest-level items (tasks) **small enough that a single person can own them**.

### Important Points

- Different processes expose **different sets of work item types** (covered next).
- Work items can be **linked into a parent–child hierarchy** (e.g., an epic containing issues containing tasks).

---

## 3. Board Processes: Basic, Agile, Scrum, CMMI

### Definition

When you create a project, Azure Boards asks which **work item process** to use. The process determines **which work item types and workflow states** your project has. Four templates are available: **Basic, Agile, Scrum, CMMI**.

### How They Differ (Complexity Increases Down the List)

| Process | Work item types (top → bottom hierarchy) | Complexity | Notable |
| --- | --- | --- | --- |
| **Basic** | **Epic → Issue → Task** | Lowest | Simplest, only 3 types. |
| **Agile** | Epic → Feature → User Story → Task (+ Bug, Issue) | Medium | Uses **User Stories**. |
| **Scrum** | Epic → Feature → **Product Backlog Item (PBI)** → Task (+ Bug, Impediment, Test Case) | Higher | Uses **PBIs** and **Impediments**. |
| **CMMI** | Epic → Feature → Requirement → Task (+ Bug, Change Request, Risk, Review) | Highest | Adds a formal **change-management** process. |

> **Important:** Choose the process based on your **organization's needs and desired complexity**. You move from simplest (Basic) to most formal (CMMI). This lesson demonstrates **Basic** first, then **Scrum**.

> **Additional Context:** The process is selected under **Advanced** options when creating a project (shown in Day 1). Once a project is created you can't switch it to a *different* base template freely, but you **can** create an **inherited process** to customize it (covered in section 14). The main difference between Agile and Scrum templates is terminology and workflow states (Agile: *User Story* with New/Active/Resolved/Closed; Scrum: *PBI* with New/Approved/Committed/Done).

---

## 4. The Basic Process Hierarchy (Epic → Issue → Task)

### Definition & Structure

The **Basic** process has three work item types arranged as a hierarchy:

1. **Epic** — the **root-level**, largest body of work (a major goal/project).
2. **Issue** — a mid-level breakdown of an epic.
3. **Task** — the **smallest** unit; should not be breakable into smaller tasks and is owned by **one person**.

### Example (Community Website Update)

- **Epic:** *"Website update for cloudopscommunity.org"* — the overall initiative.
- **Issues** (divisions of the epic): *Home page*, *About Us page*, *Secure sign-in*.
- **Tasks** (smallest, under the *Home page* issue):
  - *Design the home page header*
  - *Standardize fonts on the home page*
  - *Fix the home page CSS to make it mobile-responsive*

### Important Points

- **Epic → Issue → Task** goes from broad to granular.
- A **task** should be small enough that **accountability rests with a single person** (they can get help, but one person owns it).
- If a task still feels too big, break it into a **subtask**.

---

## 5. Hands-On: Creating a Basic Project & Board

### Steps

1. In your Azure DevOps organization, click **New project** (top-right).
2. Name it (e.g., *"Day Two Project"*), set visibility to **Private**.
3. Under **Advanced**, set **Work item process = Basic**, then **Create**.
4. Open **Boards → Boards** (left menu). This opens the default **Kanban board**.

### The Board vs Backlog Views

- **Board view (Kanban):** columns **To Do / Doing / Done**; drag-and-drop cards between columns to change state.
- **Backlog view:** items appear as a **list**; useful for creating and prioritizing items. Toggle with **"View as backlog."**

### Creating Work Items on a Basic Board

- On the board you can add **Epic** or **Issue** directly. **Tasks are created *inside* an issue** (a task is a child of an issue), not added to the board directly.
- To add a task: open (or use the ⋮ menu on) an **issue → Add task**.

> **Example (from the demo):** Create epic *"Website updates for cloudopscommunity.org"*; add issues *Website homepage*, *About Us section*, *Secure sign-in*; under *Website homepage*, add tasks like *"UI designer: add the homepage banner,"* *"Web dev: add the CSS to homepage,"* *"UI designer: standardize the font across the homepage."*

---

## 6. Anatomy of a Work Item (Fields Explained)

When you open a work item, you can fill in many fields. The important ones:

| Field | What it means |
| --- | --- |
| **Title** | Short name of the item. |
| **Iteration** | The **sprint** this item belongs to (see section 7). |
| **Description** | Details of what needs to be done. Supports rich text. |
| **Acceptance Criteria** | **Defines when the item is considered "done"** — the measurable conditions for completion. |
| **State** | Workflow status. Basic = **To Do / Doing / Done** (customizable). |
| **Tags** | Labels for filtering/grouping (e.g., `website`, `data`). |
| **Priority** | Importance ranking; e.g., **P1** (highest) … default is **P2**. |
| **Start / Target date** | Planned start and completion dates. |
| **Assigned To** | The single person accountable. |
| **Activity** | Type of work (e.g., **Design, Development, Deployment**) — used in capacity planning and card styling. |
| **Comments** | Discussion thread; **supports Markdown**; you can @-mention/assign people. |
| **Links / Parent** | Relationships to other items (e.g., a task linked to its **parent issue**). |

> **Definition — Acceptance Criteria:** A clear statement of *how you measure completion*. A common pattern: *"As a `<role>`, I will `<do something>` so that `<benefit>`."* Example: *"As a developer, I will update the website UI to be user-friendly and responsive so that users get a better experience."*

### Important Points

- **State changes two ways:** drag a card between columns **or** change the **State** field inside the item — both stay in sync.
- **A task's state depends on its parent** in normal board view: working a task implies the parent issue is in progress. *(See the clarification below — you can still move child items independently from the backlog view.)*

> **Clarification:** Early in the video the presenter says a child task **cannot** be moved to a different state independently because it's tied to its parent. He later **corrects** this: from the **Backlog item view** you **can** move individual child items (e.g., to *Approved / Committed / Done*) independently. So the accurate rule is: child items *can* be transitioned on their own; the board just also lets you move the whole parent at once for convenience.

---

## 7. Sprints / Iterations

### Definition

A **sprint** (called an **iteration** in Azure Boards) is a **fixed time-box**, typically **2–4 weeks**, during which the team commits to completing a set of work items. Think of it as a **short release**.

### How It Works

1. Plan which items go into the sprint.
2. Work the sprint for its duration (e.g., 2 weeks).
3. At the end, **measure what was achieved** and **roll over unfinished items** to the next sprint.

### Example

The default sprint is **Sprint 1**. You might set it to run **13 Nov → 27 Nov** (a 2-week sprint). An epic that spans multiple sprints can have a start date but a **blank target date** so it naturally rolls forward.

### Important Points

- Iterations are configured per project/team under **Project settings → Team configuration → Iterations** (add Sprint 2, Sprint 3, …).
- Only **added/assigned** iterations appear for a team; you must add future sprints before you can plan into them.

> **Additional Context:** Sprints come from the **Scrum** framework. A typical sprint includes ceremonies: **sprint planning** (pick the work), **daily stand-up** (progress/blockers), **sprint review** (demo results), and **retrospective** (how to improve). Azure Boards supports the planning and tracking parts of this cycle.

---

## 8. Hands-On: The Scrum Process (with Demo Data)

To explore advanced features, the video generates a realistic sample project using the **Azure DevOps Demo Generator** (link in the course repo).

### Steps to Generate Demo Data

1. Open the **Demo Generator** site → **Sign in** with your Azure account (complete **MFA** if prompted) and **grant permissions**.
2. **Choose a template** (the video uses **"Parts Unlimited"**).
3. Name the project (**"Parts Unlimited"**), select your **organization**, and **Create project**.
4. The generator builds a full project: **multiple teams, board columns, work items, and even CI/CD pipelines** with dummy data.

### Scrum Work Item Types (more than Basic)

Unlike Basic's three types, the Scrum project exposes many: **Bug, Epic, Feature, Impediment, Product Backlog Item (PBI), Task, Test Case**.

> **Definitions:**
> - **Feature:** A capability that **adds new value** to users (not a bug fix or enhancement).
> - **Product Backlog Item (PBI):** A unit of work in the backlog, usually written as a user need (*"As a customer, I want to view new tutorials"*).
> - **Impediment:** A blocker preventing progress (a Scrum-specific type).
> - **Bug:** A defect to fix.
> - **Test Case:** A test to validate behavior.

### The Scrum Hierarchy (linking items)

**Epic → Feature → PBI → Task**

Example built in the demo:

- **Epic:** *Product training*
- **Feature (child of epic):** *Training dashboard* (added via **Add link → new item → type = Feature**).
- **PBIs (under the feature):** e.g., *"As a customer, I want to view new tutorials."*
- **Tasks (under a PBI):** e.g., *"Add page for most recent tutorial"* (activity = Development, remaining work = 2h), *"Optimize data query for most recent tutorial"* (activity = Design, remaining work = 5h).

### Filtering the Board

Use the **Filter** button to narrow items by **keyword**, **type**, **assigned to**, or **state**. Example: filter by keyword `customer` to show items containing "customer." Use **Clear filters** to reset. Filters exist in both **backlog** and **feature** views.

---

## 9. Teams, Area Paths & Iteration Paths

### Teams

- When you create a project, a **default team** is created. Demo generation may add more teams.
- Create teams under **Project settings → Teams → New team** (e.g., *"Parts Unlimited Web / PUL Web"*).

### Area Path vs Iteration Path

> **Definitions:**
> - **Area Path:** A way to **organize work items by team/component/feature area** (the *"where/who"* dimension). Each team is mapped to one or more area paths.
> - **Iteration Path:** Maps work to **sprints/time-boxes** (the *"when"* dimension).

Configured under a **team → Iterations and area paths** (or **Project settings → Team configuration**):

- Assign the team the **iteration paths** (sprints) it should use.
- Assign **area paths**; enable **"Include sub areas"** (via the ⋮ menu on the area) so the team sees work items in child areas too.

> **Important:** If a team doesn't show expected sprints or items, it's usually because the needed **iterations weren't added** to that team, or **"Include sub areas"** isn't enabled for its area path.

---

## 10. Sprint Planning & Capacity

### Work Item Details Panel

In **Boards → Sprints**, enable **Work item details** (via the view's overview/options). This adds a panel summarizing **remaining work** per person and in total.

### Story Points / Remaining Work

Each task can carry a **Remaining work** estimate (in hours). The sprint view **sums** these — e.g., 2h (development) + 5h (design) = **7h pending**, broken down by activity.

> **Additional Context:** *Story points* are a relative estimate of effort/complexity (often on PBIs/user stories), while *remaining work* is an hourly estimate (usually on tasks). Azure Boards can track both. Story points feed **velocity** (work completed per sprint); remaining hours feed the **sprint burndown**.

### Capacity Planning

Open **Capacity** in the sprint view to model realistic availability:

1. **Add user(s)** to the team's capacity.
2. Set **activity + hours/day** (e.g., "Development, 1 hour/day").
3. Add **days off / vacation** (e.g., 5 days for a holiday like Diwali).

Azure computes total capacity (e.g., **1h/day × 10 working days = 10h**) and compares it against assigned work. If assigned work **exceeds capacity** (e.g., a task jumps from 2h to 11h while you're partly on vacation), the sprint shows **over-capacity in red**.

**Fix for over-capacity:** **Move the item to a future iteration** (⋮ → **Move to iteration** → e.g., Sprint 3), balancing the workload.

> **Key Takeaway:** Capacity planning turns the board from a static list into a **realistic schedule** — it flags when a team is overcommitted so work can be re-balanced across sprints.

---

## 11. Customizing the Board (Cards, Columns, Swimlanes)

Board settings (⚙ / **Settings**) let you tailor the Kanban board.

### Card Styling Rules

Color-code cards by criteria:

- **Rule example 1:** name *"Development"*, color **green**, criteria *Activity = Development* → development cards turn green.
- **Rule example 2:** name *"High priority"*, color **red**, criteria *Priority = 1* → P1 items turn red.

### Tag Colors & Annotations

- **Tag colors:** assign a color to a tag (e.g., tag `data` = yellow) so tagged cards stand out.
- **Annotations:** choose which extra info shows on cards (e.g., link to a **Test** plan).

### Columns & WIP Limits

Under **Settings → Columns**:

- Default Scrum columns: **New, Approved, Committed, Done**. You can **add columns** (e.g., *QA Approved*).
- **WIP limit (Work In Progress limit):** cap how many items a column may hold. If exceeded, the count shows in **red** (e.g., "2 of 1"). The default limit for standard columns is often **5**, preventing team overload.
- **Split a column** into **Doing / Done** sub-columns (e.g., split *QA Approved*) to track hand-offs within a stage.

> **Clarification:** In the video "WIP" is read as "work item in progress"; the standard term is **Work In Progress limit** — a Kanban technique to limit how much work is active at once, improving flow and reducing context-switching.

### Swimlanes

Add **swimlanes** (horizontal lanes) to separate items needing special attention — e.g., an **"Expedite"** lane for urgent work — so the board splits into lanes across the same columns.

> **Additional Context:** More sophisticated team boards (e.g., the *Parts Unlimited Team* board) may use stages like **New → Design → Development → Test → Done**, each split into Doing/Done, modeling a fuller delivery flow.

---

## 12. Dashboards & Widgets

### Definition

A **dashboard** is a customizable page of **widgets** giving an at-a-glance view of project/sprint health (bugs, work in progress, user stories by state, etc.).

### How to Build One

1. Go to **Overview → Dashboards → New dashboard**; name it (e.g., *"Product training"*) and pick **Team dashboard** for a team.
2. **Add widgets** (search + Add), for example:
   - **Sprint Overview** — configurable to show non-working days, count of work items, or efforts.
   - **Sprint Capacity** — shows a team's capacity for the selected sprint (e.g., PUL Web, Sprint 2).
3. **Configure** each widget's team/values, then **Done editing**.

### Important Points

- Dashboards are **team-scoped** and update as work items change.
- Widgets can also display **query charts** (see next section).

---

## 13. Queries & Charts

### Queries

**Queries** let you search/filter work items with conditions (like a database query).

**Steps:** **Boards → Queries → New query**, then build criteria in the **query editor**, e.g.:

- `Work Item Type = Task`
- `Area Path = Parts Unlimited\PUL Web`

**Save** the query (e.g., name it *"Web task"*). Save it under **Shared Queries** so it can be shared across the team/board (needed to attach it to dashboards).

### Charts

From a saved query → **Charts → New chart**:

- Choose a **chart type** (e.g., **Pie**).
- Name it (e.g., *"Web tasks by assignment"*), **Group by = Assigned To**, aggregate by **count**, sort **descending**.
- **Save chart**, then **Add to dashboard** (choose the dashboard, e.g., *Product training*).

> **Important:** To add a query chart to a dashboard, the query must live in **Shared Queries** (not your personal *My Queries*), otherwise the **Add to dashboard** option won't appear.

> **Additional Context:** Common built-in charts for Agile tracking include the **sprint burndown** (remaining work over time), **velocity** (completed work per sprint), and **cumulative flow diagram (CFD)** (items per column over time) — useful for spotting bottlenecks.

---

## 14. Customizing the Process (Inherited Processes)

### Definition

You cannot edit the **system default** processes (Basic/Agile/Scrum/CMMI) directly, but you can create an **inherited process** — a copy you *can* modify (add fields, states, rules, work item types) — and apply it to projects.

### Steps (add a custom field)

1. **Organization settings → Process**.
2. Select a base process (e.g., **Scrum**) → **⋮ → Create inherited process**; name it (e.g., *"Customized Scrum"*).
3. Open it → pick a work item type (e.g., **Product Backlog Item**) → **New field** (e.g., *"Ticket ID"*), optionally create a **new field group** (e.g., *"Parts Unlimited"*).
4. Apply it: **All processes → Scrum → Projects → ⋮ → Change process** → target = **Customized Scrum**.
5. Now open a PBI in that project — the new **Ticket ID** field appears; you can fill it (e.g., `1234`) and **query** work items by it.

> **Key Takeaway:** Inherited processes let you adapt Azure Boards to your organization's terminology and data needs (custom fields, states, work item types) **without breaking** the built-in templates.

---

# Quick Revision

### Key Concepts

- **Azure Boards** = the Agile planning/tracking service in Azure DevOps (like Jira/Notion; an "advanced to-do list").
- **Work item** = the trackable, assignable unit of work (epic, feature, issue, PBI, task, bug, etc.).
- **Processes** (increasing complexity): **Basic → Agile → Scrum → CMMI**; each defines its own work item types and states.
- **Basic hierarchy:** **Epic → Issue → Task**; **Scrum hierarchy:** **Epic → Feature → PBI → Task**.
- **Task** = smallest, single-owner unit; break bigger work into subtasks.
- **Sprint (iteration)** = 2–4 week time-box; unfinished work rolls to the next sprint.
- **Area path** = organize by team/component; **iteration path** = organize by sprint/time.
- **Capacity planning** = model availability (hours/day, days off) to flag over-commitment (shown in red).
- **Board customization:** styling rules, tag colors, columns, **WIP limits**, split columns, **swimlanes**.
- **Dashboards + widgets**, **queries + charts** (share via **Shared Queries**), and **inherited processes** for custom fields.

### Important Definitions

- **Work Item:** A unit tracking one activity (assignable, with a state).
- **Epic:** Top-level, largest body of work (a major goal).
- **Issue (Basic):** Mid-level breakdown of an epic.
- **Feature (Scrum/Agile):** A capability adding new user value.
- **Product Backlog Item (PBI):** A backlog work unit, often a user need.
- **Task:** Smallest, single-owner work unit.
- **Impediment:** A blocker (Scrum type).
- **Acceptance Criteria:** Conditions that define when an item is "done."
- **Sprint / Iteration:** A fixed time-box (2–4 weeks) for a set of work.
- **Area Path:** Organizes work by team/component/area.
- **Iteration Path:** Maps work to sprints.
- **WIP Limit (Work In Progress):** Max items allowed in a column to keep flow healthy.
- **Swimlane:** A horizontal board lane to separate categories of work (e.g., Expedite).
- **Inherited Process:** An editable copy of a base process for customization.

### Important Comparisons

**Board processes**

| | Basic | Agile | Scrum | CMMI |
| --- | --- | --- | --- | --- |
| Complexity | Lowest | Medium | Higher | Highest |
| Mid item | Issue | User Story | PBI | Requirement |
| Special | — | — | Impediment | Change mgmt (Change Request, Risk) |

**Story points vs remaining work**

| | Story Points | Remaining Work |
| --- | --- | --- |
| Measures | Relative effort/complexity | Estimated hours left |
| Usually on | PBI / User Story | Task |
| Feeds | Velocity | Burndown / capacity |

### Common Mistakes / Misconceptions

- **Thinking child items can't change state independently.** They can — use the **Backlog item view** to move individual children (the video corrects this).
- **Not adding iterations to a team**, then wondering why future sprints don't appear.
- **Forgetting "Include sub areas"**, so a team doesn't see work items in child area paths.
- **Saving a query in "My Queries"** and being unable to add its chart to a dashboard — it must be in **Shared Queries**.
- **Ignoring WIP limits/capacity**, leading to overloaded columns/teams (shown in red).
- **Making tasks too large.** A task should be a single-person, non-divisible unit.

### Interview / Exam Points

- Name the **four process templates** and how their complexity/work items differ.
- Explain the **Basic vs Scrum hierarchies** (Epic→Issue→Task vs Epic→Feature→PBI→Task).
- Define **area path vs iteration path**.
- What is a **sprint/iteration**, and how long is it typically?
- Explain **capacity planning** and how over-capacity is handled (move to a future iteration).
- Explain **WIP limits** and **swimlanes** and why they help flow.
- How do you build a **dashboard** and add a **query chart** (and why the query must be **shared**)?
- What is an **inherited process**, and why can't you edit the base processes directly?
- Difference between **story points** and **remaining work**.

### Final Takeaways

1. Azure Boards is the **Agile planning hub** of Azure DevOps — a powerful, visual, shared to-do system.
2. **Work items** are the core; their available **types depend on the chosen process** (Basic → CMMI).
3. Break work top-down: **Epic → Feature/Issue → PBI → Task**, keeping tasks small and single-owner.
4. **Acceptance criteria** make "done" objective and measurable.
5. **Sprints/iterations** time-box work; unfinished items roll forward.
6. **Area paths** (who/where) and **iteration paths** (when) organize and route work to teams.
7. **Capacity planning** models real availability and flags over-commitment for re-balancing.
8. The **Kanban board is highly customizable**: styling rules, tag colors, columns, WIP limits, split columns, swimlanes.
9. **Dashboards, widgets, queries, and charts** turn tracked data into insight (share queries to reuse them).
10. **Inherited processes** let you extend Azure Boards (custom fields/types) without touching the built-in templates.
