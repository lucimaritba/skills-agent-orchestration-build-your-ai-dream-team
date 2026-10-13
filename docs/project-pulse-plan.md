# Project Pulse Implementation Plan

## Goal and Requirements

Build a lightweight static dashboard that helps Mona's contributors quickly understand which projects are active, who owns them, their status, recent activity, and priority or risk. The first view must clearly present a polished Project Pulse dashboard with readable project cards, status badges, and responsive spacing.

Use a top-level `projects` array in `app/project-data.json`. Each project must include `name`, `owner`, `status`, `recentActivity`, and `priority`. The app must render project data in the browser and provide a visible fallback for loading errors or an empty project list.

## Responsibilities

- **Planner:** Define implementation phases, file ownership, dependencies, parallel work, edge cases, and validation criteria.
- **Designer:** Set the dashboard's information hierarchy, visual direction, accessibility expectations, and responsive behavior. Review the integrated experience and report design tradeoffs or issues.
- **Coder:** Implement the assigned static app and launch configuration, follow the agreed design and data contracts, and validate the result.
- **Orchestrator:** Assign non-overlapping scopes, coordinate phase handoffs, resolve integration issues, and verify the final dashboard.

## Ordered Implementation Phases

1. **Agree on the contracts.** Planner and Designer confirm the required information hierarchy, responsive behavior, accessibility expectations, project fields, and stable status and priority labels. Orchestrator records the contracts for the Coder.
2. **Implement the app files.** Coder creates `app/project-data.json`, `app/index.html`, and `app/styles.css` using the agreed data and UI contracts. The page uses the exact title `Project Pulse`, references the stylesheet and JSON data, and renders each project with the `project-card` class.
3. **Add the preview configuration.** Coder creates `.vscode/launch.json` as strict JSON without comments. Add a configuration named `Run Project Pulse Dashboard` that serves from the `app/` directory and opens `index.html`, not a directory listing.
4. **Integrate and validate.** Orchestrator checks all files together, runs the available structural checks, launches the preview, and reports any remaining issues or assumptions.

## File Assignments

- `app/project-data.json` — **Coder:** Provide a top-level `projects` array. Each record includes `name`, `owner`, `status`, `recentActivity`, and `priority`; use representative static data unless Mona supplies a source dataset.
- `app/index.html` — **Coder:** Set the exact document title to `Project Pulse`; link `styles.css`; load `project-data.json`; render visible project cards and all required project fields. Use semantic structure and provide loading, empty, and error states.
- `app/styles.css` — **Coder, guided by Designer:** Implement the approved visual direction and responsive behavior. Include `.dashboard` and `.project-card` selectors, clear status and priority treatments, readable spacing and typography, border radius, and box shadow.
- `.vscode/launch.json` — **Coder:** Use strict JSON with no comments. Configure `Run Project Pulse Dashboard` to run `python3 -m http.server 5500` with its working directory set to `${workspaceFolder}/app`. Configure `serverReadyAction` to open `http://localhost:%s/index.html`.

Designer supplies guidance and reviews the experience; Coder owns implementation of the four assigned files. Keep these file scopes explicit to prevent conflicting edits.

## Dependencies and Work Ordering

The project data schema and visual/UI contracts must be agreed before implementation. The HTML depends on the agreed JSON field names and CSS class hooks; CSS depends on the agreed layout and hooks. The launch configuration depends on the app directory, server command, port, and target URL being fixed.

After those contracts are set, preparing the sample JSON and finalizing the design direction can run in parallel because they have separate owners and files. The launch configuration can also be prepared in parallel with app implementation once its command and URL are fixed. HTML and CSS work may proceed in parallel only after their shared class and layout contracts are stable. Integrated browser validation must run after all four files are complete.

## Edge Cases and Open Questions

- Handle an empty `projects` array, malformed or unavailable JSON, and unknown status or priority values without leaving the page blank.
- Check long project names, activity summaries, and owner names at narrow viewport widths.
- The brief specifies static JSON but no live data source. Use representative project entries for the exercise and confirm with Mona before connecting real project data.
- Port `5500` may already be occupied; if so, resolve the conflict and ensure the browser opens the matching server URL.

## Validation Expectations

- **Content:** Confirm the page title is exactly `Project Pulse`; multiple projects are visible; each card shows name, owner, status, recent activity, and priority.
- **Data:** Parse `app/project-data.json` as JSON; verify the top-level `projects` value is an array and every project has all five required fields.
- **Visual and accessibility behavior:** Review the dashboard at desktop and narrow mobile widths; verify readable contrast, semantic structure, keyboard-accessible content, clear status and priority distinctions, and no clipped or overlapping text. Check loading, empty, and data-error states.
- **Launch:** Parse `.vscode/launch.json` as JSON; confirm the exact launch name, command, working directory, and server-ready URL. Start `Run Project Pulse Dashboard` and verify the browser opens `http://localhost:<port>/index.html` and displays the dashboard rather than a directory listing.
- **Final integration:** Review all four assigned files together and report any unmet checks or assumptions.