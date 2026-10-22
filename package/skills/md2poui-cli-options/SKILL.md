---
name: md2poui-cli-options
description: Change or test md2poui CLI arguments and option forwarding while preserving library overloads, defaults and filesystem error behavior.
---

# CLI and library contract

Read [the inspected contract](references/contract.md) and revalidate the task revision. Trace src/bin/md2poui.ts -> src/index.ts -> src/options.ts; Graphify can identify callers when available, but source decides current behavior.

Distinguish an omitted option, explicit false, an empty string and invalid input. Check the parser name, argv value, Options assignment and library default separately. Never replace explicit false with a default.

Preserve both library overloads: Markdown text to HTML and existing filesystem source to generated files. A CLI path error must not silently become Markdown input. Keep the current nonzero exit and error output unless the requirement explicitly changes them.

For a parser change, exercise the compiled CLI using process.execPath, an argument array, owned temporary directories, a timeout, exit status, stderr and generated artifacts. A library-only test does not cover the parser. For booleans, exercise omitted, positive and negative values. Include meaningful missing/invalid inputs and preservation of existing output when relevant.

Use public expected output, not assertions that mirror argv assignments. Run npm test in the owned checkout. Preserve existing tests and exclude dist, test/result and graph outputs from the commit. Do not update dependencies or replace the parser without a task-specific need.
