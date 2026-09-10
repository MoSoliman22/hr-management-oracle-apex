# HR Management System — Oracle APEX

A full-stack HR administration application built in **Oracle APEX 24+**, using the classic Oracle **HR sample schema** (OEHR-prefixed tables). Built as a portfolio project to demonstrate low-code application development, PL/SQL, data modeling, and workflow automation.

🎥 **[Watch the demo video](https://www.loom.com/share/0a5360bf2151436bb3d6b3f2aeb385cf)** &nbsp;|&nbsp; 💼 **[Connect on LinkedIn](https://www.linkedin.com/in/soliman97/)**

---

## Overview

This app goes beyond a basic CRUD demo — it's a complete HR management workflow: dashboards, employee/department/job administration, an interactive org chart, role-based access control, and automated email notifications triggered through an external automation platform (n8n).

---

## Features

### 📊 Interactive Dashboard
- KPI cards with animated, scroll-triggered counters (IntersectionObserver)
- Bar and pie charts for headcount by department and salary distribution by job
- Recent Hires and Top Paid Employees side-by-side report panels

### 👥 Employee, Department & Job Management
- Interactive Reports with joined SQL for human-readable data (job titles, department names, manager names — not raw foreign key IDs)
- Forms with Select List items for all foreign key fields
- Full CRUD with validation

### 🌳 Org Chart
- Native APEX Tree region built from the `MANAGER_ID` → `EMPLOYEE_ID` hierarchy
- Click any node to open that employee's full profile

### 🧑‍💼 Employee Detail / Profile Page
- Full employee info, job history, and direct reports in a single view
- Linked from both the Employees report and the Org Chart

### 🔐 Authentication & Access Control
- Custom authentication scheme
- Role-based authorization restricting destructive actions (e.g., delete) to admin users

### 🤖 Workflow Automation (n8n Integration)
- When a new employee is created, APEX calls an n8n webhook via `APEX_WEB_SERVICE` + `APEX_JSON`
- n8n automatically sends the employee's manager a notification email — zero manual steps

### 🎨 Custom UI
- Fully custom CSS theme (moved away from default Redwood styling)
- Toast notifications on form submit
- Responsive, polished layout across all pages

---

## Tech Stack

| Layer | Technology |
|---|---|
| Application Platform | Oracle APEX 24+ |
| Database | Oracle Database (HR sample schema, `OEHR_*` tables) |
| Backend Logic | PL/SQL |
| Automation | n8n (webhooks, REST) |
| Styling | Custom CSS |
| Interactivity | JavaScript (Dynamic Actions, IntersectionObserver) |

---

## Pages

| Page | Description |
|---|---|
| Dashboard | KPIs, charts, recent hires, top paid employees |
| Employees | Interactive Report + Form |
| Departments | Interactive Report + Form |
| Jobs | Interactive Report + Form |
| Org Chart | Tree region, hierarchy view |
| Analytics | Additional charts and breakdowns |
| Employee Detail | Profile, job history, direct reports |
| Login | Custom authentication |

---

## Repository Contents

```
├── app/
│   └── f101.sql              # Exported APEX application
├── css/
│   └── hr-app-custom.css     # Custom app-wide styling
├── automation/
│   └── new-employee-workflow.json   # n8n workflow export
├── screenshots/
│   └── ...                   # App screenshots
└── README.md
```

---

## Setup / Import Instructions

1. Requires an Oracle Database with the **HR sample schema** installed (tables prefixed `OEHR_`)
2. In Oracle APEX App Builder, go to **App Builder → Import**
3. Upload `app/f101.sql`
4. Follow the install wizard, selecting your target workspace and schema
5. (Optional) Import `automation/new-employee-workflow.json` into your own n8n instance to enable the manager-notification email feature
6. Apply `css/hr-app-custom.css` via **Shared Components → User Interface Attributes → CSS**

---

## Key Technical Notes

- Interactive Reports use joined SQL queries so foreign keys display as readable names instead of raw IDs
- The Org Chart uses APEX's native Tree region, sourced from a self-referencing `MANAGER_ID` hierarchy on the Employees table
- New employee creation triggers an `Execute Code` process that builds a JSON payload with `APEX_JSON` and posts it to an n8n webhook via `APEX_WEB_SERVICE.MAKE_REST_REQUEST`
- Local Oracle XE instances require an explicit network ACL grant (`DBMS_NETWORK_ACL_ADMIN`) before outbound HTTP calls will succeed

---

## Author

Built by **Soliman** as a portfolio project.
Connect on [LinkedIn](https://www.linkedin.com/in/soliman97/) — feel free to reach out with feedback or questions.
