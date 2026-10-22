---
name: md2poui-markdown-rendering
description: Change or test md2poui Markdown rendering, titles, escaping, links and asset rewriting using fixtures and observed generated HTML.
---

# Markdown rendering

Read [the rendering map](references/rendering.md). Trace Converter.convert/renderComponentView -> Transform.textToIcon -> marked/PoRenderer -> componentView. Confirm Graphify relationships in current source when the graph is available.

Choose the public entry that exercises the requirement: text conversion and directory generation differ in options, title fallback and asset copying. Use small fixtures for first H1, later H1, H2 and no H1 when titles change. Check page title, remaining body and menu label independently.

For escaping, exercise code blocks and inline code containing <, >, &, quotes and Angular braces as relevant. Derive expected public output from the requirement; do not copy the escape algorithm. Escaping code is not sanitizing arbitrary HTML.

For links, separate external URLs, relative .md, fragments and directory names. For assets, create real files in owned temporary fixtures, exercise copying on/off, verify copied bytes and the generated path. UUID-based names must correspond between HTML and disk; do not require a literal UUID.

When absent assets, multiple src attributes or raw HTML enter scope, define their expected behavior before changing it. Avoid incidental security or compatibility rewrites without a demonstrated issue. Run npm test and describe exactly which output paths were exercised; never claim an Angular browser test from generated strings alone.
