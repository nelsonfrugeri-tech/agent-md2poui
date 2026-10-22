---
name: md2poui-onboarding
description: Explain md2poui to a new contributor and identify its actual repository, conversion entry points, project commands and relevant domain skills before a change.
---

# md2poui onboarding

Start with the user's task and the checkout's current revision. Read [the project map](references/project-map.md), then inspect the named files in that checkout; the map is a versioned observation, not an evergreen runtime guarantee.

Explain only what helps this contributor start: md2poui is a TypeScript Node library/CLI that turns Markdown into Angular/PO-UI source files. This repository is not a running Angular app. Identify the two library modes and where CLI options enter the pipeline.

Use GitHub for current repository/task context when available, Trello for the selected story and Notion for its ADR. Discover actual tools and authorized resources before calling them. Graphify helps navigate an existing graph; confirm the code. Use deja-vu only for a pertinent earlier decision. Report unavailable sources and distinguish local analysis from remote reads.

Choose the next skill by the change:

- `agent-md2poui:md2poui-cli-options`: argument parsing, defaults, forwarding and filesystem errors.
- `agent-md2poui:md2poui-markdown-rendering`: title, Markdown, escaping, links and assets.
- `agent-md2poui:md2poui-angular-generation`: output files, component identity, home, routes and menus.
- `agent-md2poui:code-review`: an independent review of a concrete diff.

Read package.json and gulpfile.js before running commands. `npm test` removes test/result, compiles src into dist and runs Mocha; use an owned checkout for validation when shared outputs might interfere. If dependencies are absent, an authorized `npm ci --ignore-scripts` belongs in that isolated checkout. Never mutate another session's node_modules. Do not invent a Make target, lint script or Angular dev server.

Conclude a walkthrough with the relevant entry file, one concrete next step and any unknowns. Do not implement a tutorial feature or create a PR unless requested.
