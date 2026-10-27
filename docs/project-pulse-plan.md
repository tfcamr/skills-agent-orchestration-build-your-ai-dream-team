# Project Pulse implementation plan

## Goal

Build Mona's lightweight static Project Pulse dashboard so contributors can scan active projects, owners, status, recent activity, priority or risk, and a short contributor-friendly summary. The page should render a clear project-card layout and run from the VS Code **Run Project Pulse Dashboard** launch configuration.

## File assignments

| File | Owner | Responsibility and expected result |
| --- | --- | --- |
| `app/styles.css` | **Designer** | Define the responsive visual system, information hierarchy, spacing, readable typography, status and priority treatments, and accessible focus and contrast. Style the agreed `.dashboard` and `.project-card` hooks, including polished borders and shadows. |
| `app/project-data.json` | **Coder** | Provide strict JSON with a top-level `projects` array. Each project includes `name`, `owner`, `status`, `recentActivity`, and `priority`, plus a concise contributor-friendly summary. |
| `app/index.html` | **Coder** | Build the Project Pulse page, load `project-data.json`, and render the project details and summaries using the agreed class hooks. Keep status and priority understandable without relying on color alone. |
| `.vscode/launch.json` | **Coder** | Add strict JSON configuration named exactly **Run Project Pulse Dashboard**. Serve from `${workspaceFolder}/app` and open `index.html`, rather than showing a directory listing. |

## Phases and responsibilities

1. **Agree on the interface contract.** The Orchestrator confirms the data fields and HTML/CSS class hooks with Designer and Coder before implementation. At minimum, the page has a `.dashboard` root and `.project-card` for each project.
2. **Implement in parallel after the contract.** The Designer owns only `app/styles.css`. The Coder owns `app/project-data.json`, `app/index.html`, and `.vscode/launch.json`; the Coder defines the data first and then renders it in the page.
3. **Integrate.** The Orchestrator checks that HTML class hooks match the CSS and that rendered fields match the JSON schema. Any corrections go to the owner of the affected file.
4. **Validate and report.** The Orchestrator runs the checks below and summarizes the runnable result and any remaining limitations.

## Dependencies and parallel work decisions

- `app/index.html` depends on the JSON schema in `app/project-data.json` and the class hooks agreed with the Designer.
- `app/styles.css` depends on the agreed class hooks, but not on the completed HTML, so the Designer and Coder can work in parallel after the contract is set.
- `.vscode/launch.json` depends on the app location and entry page, not on the dashboard content; the Coder can create it alongside the app files.
- Integration depends on all four assigned files and runs after implementation. Validation runs after integration so it checks the combined result.
- File ownership does not overlap: Designer changes only the stylesheet; Coder changes the data, HTML, and launch configuration; Orchestrator coordinates and verifies rather than implementing these files.

## Validation expectations

- Parse `app/project-data.json` and `.vscode/launch.json` as JSON.
- Confirm the data has a top-level `projects` array and every project includes `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Confirm `app/index.html` loads the stylesheet and project data and displays the expected project fields in `.project-card` elements under `.dashboard`.
- Confirm `app/styles.css` styles `.dashboard` and `.project-card`, includes responsive layout and visible status/priority treatments, and provides readable spacing, contrast, and keyboard focus.
- Confirm the launch configuration has the exact name **Run Project Pulse Dashboard**, serves from `app/`, and opens `index.html`.
- Launch the dashboard and verify the browser shows the Project Pulse UI rather than a directory listing. Check the layout at desktop and mobile widths, keyboard navigation, and the browser console.
- Handle an empty project list or a data-loading error with a clear message; status and priority must remain understandable without color alone.
