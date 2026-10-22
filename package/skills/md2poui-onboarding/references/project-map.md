# Inspected project map

Inspected on 2026-10-22 at fork commit [9b65624b9b8c9e27ee73e279eeef2afffbcde269](https://github.com/nelsonfrugeri-tech/md2poui/tree/9b65624b9b8c9e27ee73e279eeef2afffbcde269). Revalidate against the current checkout. Upstream is [totvs/md2poui](https://github.com/totvs/md2poui); development targets the user-authorized fork.

## Flow

`src/bin/md2poui.ts` -> `src/index.ts`/`src/options.ts` -> `src/converter.ts` -> `src/component.ts`, `src/renderer/poRenderer.ts` and `src/templates/*`.

- CLI: yargs parses srcPath/destDir, forwards options including home, rejects missing source/destination and a destination that is a file, and reports failures with a nonzero exit.
- Library: `md2poui(markdown)` returns HTML; `md2poui(srcPath, destDir, options)` writes files. `isFileOrDirectory` chooses the mode, so a nonexistent string can be treated as Markdown by the library. Do not move CLI-only validation into that overload accidentally.
- Options: defaults includes home, createHelpers, recursive, flatDirs and copyExternalFiles all true. `adjustOptions` resolves exclusions and renders Mustache placeholders. The resource-folder/path comments do not match the respective values; read defaultOptions.
- Converter: writes home when enabled, discovers Markdown, constructs Components and emits class/view pairs, then emits module/routing/service when createHelpers is enabled. It is synchronous and has no whole-conversion rollback.
- Component: identity is derived from the relative directory, not the Markdown filename. flatDirs changes physical output and hierarchy. Changing identity affects imports, routes, class names and menu links.
- Renderer: marked plus PoRenderer transforms headings, code, links and images. The first nonempty H1 becomes the page title and is removed from body output. Directory conversion falls back to Component.getClassName when there is no H1; Markdown-text conversion keeps the empty title.
- Templates: Mustache returns TypeScript/HTML strings. Generating a file is not proof that an Angular application compiles or renders it.

## Repository conventions and commands

package.json declares TypeScript ^4.9.4, marked ^4.2.12, Mustache ^4.2.0, yargs ^17.6.2 and Mocha ^10.2.0. These are declared ranges, not a claim about every installed version. tsconfig.app.json compiles src/**/*.ts to dist; CommonJS, strict=true with strictNullChecks=false. Tests are CommonJS JavaScript under test/ and import ../dist. Match the existing structure; add no application framework or dependency upgrade for an unrelated change.

From the code repository root:

- `npm test`: pretest runs `npx gulp pretest && npx tsc --p tsconfig.app.json`; gulp deletes test/result; Mocha runs ./test. It does not delete all of dist first.
- `npm run build`: prebuild deletes dist; TypeScript compiles; postbuild copies package.json/README and runs npm pack ./dist. This mutates output and creates an archive; it is not an extra read-only check.
- `node dist/bin/md2poui.js <source> <destination> --no-home`: real compiled CLI; choose temporary owned input/output when exercising it.

Existing tests: component.spec.js and helpers.spec.js compare simple generated artifacts to templates; cli.spec.js exercises the compiled process and input errors; title.spec.js covers no-H1 fallback, first H1, --no-home and unchanged text overload. Do not copy production templates into new expected values when independent output assertions can detect the bug.

CLI arguments/home were already corrected in commit 4e19cec. No-H1 directory title fallback was already implemented in 9b65624. Do not propose either as an unimplemented demo challenge without inspecting a different target revision.
