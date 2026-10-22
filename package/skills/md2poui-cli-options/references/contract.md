# Inspected CLI contract

Source: [md2poui 9b65624](https://github.com/nelsonfrugeri-tech/md2poui/tree/9b65624b9b8c9e27ee73e279eeef2afffbcde269), inspected 2026-10-22. Verify current revision before using this map.

- src/bin/md2poui.ts declares positional srcPath/destDir, reads the same names, forwards home and the other exposed options, checks source existence and rejects a destination file. Its catch writes an error and sets process.exitCode=1. cli.spec.js exercises this process path, including --home and --no-home.
- src/index.ts exports CommonJS via `export = md2poui`. isFileOrDirectory uses lstatSync; stat failure selects textual conversion. adjustOptions applies defaults, resolves exclusions against srcPath and renders string placeholders with Mustache.
- src/options.ts defaults: exclusions/imports=[], flatDirs/recursive/createHelpers/home/copyExternalFiles=true, highlightClassName=highlight, moduleName=docs, parentRoutePath={{moduleName}}, resourceFolderName=assets, resourcePathName=app/{{moduleName}}/{{resourceFolderName}}. The two resource comments are swapped relative to these values.
- Text overload has no options parameter in its public signature. File conversion and textual conversion do not share all initialization behavior.
- npm test compiles before Mocha. npm run build also cleans dist and packages it; inspect command effects before running.

The earlier srcPath/source mismatch and missing home forwarding are already fixed at this revision. Requirements for another error path or transactional output still need an explicit expected result and a reproducer.
