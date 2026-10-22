---
name: md2poui-angular-generation
description: Change or test md2poui generated Angular components, routes, menus and home artifacts, including flatDirs, recursion and exclusions.
---

# Angular artifact generation

Use for Converter, Component or template changes. Read [artifact relationships](references/artifacts.md) and revalidate the current revision.

Trace selected Markdown -> Component identity -> class/view -> module, routing and menu service. Use Graphify if available to locate relations, then read the relevant source. Select fixtures that distinguish the option being changed: root/nested directories, excluded file/directory, flatDirs or recursion on/off.

For home, check both .ts/.html files and their imports, declarations and routes. For createHelpers, inspect module, routing and service together. These flags are independent in the inspected code; do not invent a new dependency. Match physical paths, relative imports, class names and route names for the same component.

Names derive from directories, not Markdown filenames. When flattening or multiple Markdown files matter, reproduce possible collisions before proposing a naming policy. For menu changes check title/class-name fallback, parentRoutePath and hierarchical subItems. If string templates change, include relevant quote/brace cases and check generated syntax independently of the production template.

Exercise the real library or CLI in an owned temporary directory and assert actual generated artifacts. A Mustache-only test cannot prove discovery, naming or writing behavior. Run npm test. Do not install a complete Angular app just to test file selection; perform and report Angular compilation separately only when required by the task. Keep dist, test/result and graph outputs out of the commit.
