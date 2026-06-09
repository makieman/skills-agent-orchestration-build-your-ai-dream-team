# Project Pulse dashboard implementation plan

## Summary
Build a small static dashboard in `app/` that shows Project Pulse project cards from `app/project-data.json`, uses polished responsive styling in `app/styles.css`, and opens correctly from `.vscode/launch.json` as **Run Project Pulse Dashboard**.  
Assumption: keep all app behavior in the existing file set only; no extra JS file is in scope, so the page logic should live in `app/index.html`.

## Roles

### Designer responsibilities
- Define the information hierarchy for the dashboard.
- Specify card layout, spacing, typography, badges, and responsive behavior.
- Ensure accessibility basics: readable contrast, semantic structure, clear states.
- Review `app/index.html` and `app/styles.css` for visual consistency and usability.

### Coder responsibilities
- Implement the static dashboard files exactly in scope.
- Wire `app/index.html` to load/render the project data.
- Create valid `app/project-data.json` with the required schema.
- Create strict JSON `.vscode/launch.json` that serves from `app/` and opens `index.html`.
- Keep implementation deterministic and easy to validate.

## Ordered implementation steps

| # | Step | Owner | Files | Output |
|---|---|---|---|---|
| 1 | Finalize dashboard structure, data shape, and launch behavior | Designer + Coder | none | Shared implementation rules for cards, fields, and preview flow |
| 2 | Implement dashboard markup and data rendering | Coder (Designer review) | `app/index.html` | Title, linked CSS/data, visible project cards, required fields rendered |
| 3 | Implement polished responsive styling | Designer direction, Coder implementation | `app/styles.css` | `.dashboard`, `.project-card`, badges, spacing, shadows, responsive layout |
| 4 | Create project seed data | Coder | `app/project-data.json` | Valid JSON with top-level `projects` array and required fields |
| 5 | Add VS Code launch configuration | Coder | `.vscode/launch.json` | Strict JSON launch profile named exactly `Run Project Pulse Dashboard` |
| 6 | Validate end-to-end behavior | Orchestrator + Coder | all above | Dashboard opens from `index.html`, not a directory listing |

## File assignments

| File | Primary owner | Secondary owner | Notes |
|---|---|---|---|
| `app/index.html` | Coder | Designer | Must include Project Pulse title, reference CSS/data, and render project cards with `status`, `recentActivity`, and `priority`. |
| `app/styles.css` | Coder | Designer | Must include `.dashboard` and `.project-card`, plus polished responsive styling (`border-radius`, `box-shadow`). |
| `app/project-data.json` | Coder | Designer | Must use a top-level `projects` key and include `name`, `owner`, `status`, `recentActivity`, `priority`. |
| `.vscode/launch.json` | Coder | Orchestrator | Must be strict JSON, serve from `app/`, and open `http://localhost:%s/index.html`. |

## Dependencies

1. `app/index.html` depends on the agreed data fields and layout direction.
2. `app/styles.css` depends on the final card structure and class names from `app/index.html`.
3. `app/project-data.json` depends on the agreed schema only; it can be drafted early.
4. `.vscode/launch.json` depends on the fixed preview approach: `app/` as working directory, port `5500`, and `index.html` as the open target.
5. Validation depends on all four files being complete and consistent.

## Parallel work decisions

- **Can run in parallel:**  
  - Designer review of layout/styling direction can happen while Coder drafts `app/project-data.json` and `.vscode/launch.json`.
- **Should not overlap:**  
  - Final edits to `app/index.html` and `app/styles.css` should be coordinated to avoid conflicting card structure and CSS hooks.
- **Best parallel split:**  
  - One stream: HTML/CSS implementation.  
  - Second stream: JSON data + launch config.

## Sequential work

1. Lock the field schema and card layout.
2. Build `app/index.html`.
3. Align `app/styles.css` to the final markup.
4. Fill `app/project-data.json`.
5. Add `.vscode/launch.json`.
6. Run validation and adjust only if checks fail.

## Edge cases to handle

- Empty or missing `projects` array.
- Missing required fields in any project record.
- Long project names or activity text wrapping poorly.
- Status/priority values that need readable badge treatment.
- JSON parse failures in `app/project-data.json` or `.vscode/launch.json`.
- Launching the app from the repo root instead of `app/`, which would show a directory listing instead of the dashboard.
- Small-screen layout where cards must stack cleanly.
- Data fetch/render failure in the static page; show a simple fallback state.

## Validation expectations

- `app/index.html` contains **Project Pulse**.
- `app/index.html` references `styles.css` and `project-data.json`.
- `app/index.html` renders visible cards with the `project-card` class.
- `app/index.html` shows `status`, `recentActivity`, and `priority`.
- `app/styles.css` includes `.dashboard`, `.project-card`, `border-radius`, and `box-shadow`.
- `app/project-data.json` parses as JSON and includes a top-level `projects` key.
- Each project includes `name`, `owner`, `status`, `recentActivity`, and `priority`.
- `.vscode/launch.json` parses as JSON.
- Launch name is exactly `Run Project Pulse Dashboard`.
- Launch serves from `app/` and opens `index.html`, not a directory listing.
- Manual preview confirms the dashboard opens in the browser and looks polished.

## Open questions

- None blocking. If needed, choose a small representative seed set (for example 3–5 projects) with varied statuses and priorities.
