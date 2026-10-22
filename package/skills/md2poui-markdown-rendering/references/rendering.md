# Inspected rendering behavior

Source: [md2poui 9b65624](https://github.com/nelsonfrugeri-tech/md2poui/tree/9b65624b9b8c9e27ee73e279eeef2afffbcde269), inspected 2026-10-22. Revalidate current code.

PoRenderer stores title/assets per instance. Its first nonempty H1 sets title and returns an empty body fragment; later headings emit HTML. Converter.renderComponentView sets Component title to renderer.getTitle() || component.getClassName(), and both page and menu use that title. Converter.convert(markdown) does not apply that directory fallback. test/title.spec.js covers this distinction, including --no-home.

componentView.ts uses Mustache escaping for title and unescaped {{&content}} for rendered content. Transform.textToIcon runs before marked. escapeCode replaces ampersand, double quote, angle brackets and braces; escapeCodespan replaces braces, while marked handles part of inline processing. Test through the public entry.

link treats href without `http` containing `.md` as an internal route derived from the final directory segment. Others receive href, target=_blank and rel=noopener noreferrer. This heuristic is not a general URL classifier.

image records relative assets when copyExternalFiles is true, generates UUID v1 plus extension and uses resourcePathName. Converter.copyFiles copies from each Markdown file's directory into output/resourceFolderName. html also searches src with a regex; it is not a full HTML parser. adjustResourceHtml wraps images in a span.

sanitize-html is used by adjustTitleToFragment, whose heading caller is commented out. Its import does not prove general HTML sanitization. The text overload creates a renderer without adjustOptions; do not assume every filesystem default is applied there.
