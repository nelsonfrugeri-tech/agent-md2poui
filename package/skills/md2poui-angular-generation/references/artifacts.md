# Inspected artifact relationships

Source: [md2poui 9b65624](https://github.com/nelsonfrugeri-tech/md2poui/tree/9b65624b9b8c9e27ee73e279eeef2afffbcde269), inspected 2026-10-22. Check current source before changing behavior.

Converter.execute creates home first when enabled, discovers Markdown, writes each Component class/view, then module/routing/service when createHelpers=true. There is no whole-run rollback. getMarkdownFiles handles a file directly, otherwise walks directories subject to recursive, extension .md and exclusions. Exclusions use both exact paths and dirname prefixes; test similar prefixes if relevant.

Component derives relative directory, optional flatDirs final segment, name and PascalCase class. adjustDirname uses the existing numeric-prefix regex; do not infer that it handles all numeric naming schemes. Multiple files in one directory can share output identity.

module.ts and routing.ts condition home imports/declarations. With home, component routes are children; without it, they are direct routes. Wildcard redirects to the first component. Empty input needs its own expected behavior if in scope.

loadMenuItems uses Component title or class name, prefixes links with parentRoutePath if nonempty, and searches previously accumulated parents when flatDirs=false. menuItem.ts recursively renders subItems; service.ts exposes getMenuItems. Component title now receives the directory-generation no-H1 fallback before service rendering.

component.spec.js/helpers.spec.js cover basic fixtures through the library; cli.spec.js and title.spec.js cover compiled CLI options and title output. These checks compile the converter's TypeScript, not an Angular application consuming generated output.
