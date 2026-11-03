# Building and editing the TeX sources

These sources produce the three reading editions in [`../pdf/`](../pdf/).
They include the German text, editorial notes, index and layout definitions.
They are self-contained apart from a TeX installation and the required fonts.

## Requirements

Use **LuaLaTeX** and **latexmk** with the following LaTeX packages:
`fontspec`, `amsmath`, `unicode-math`, `babel` (German and polytonic Greek),
`microtype`, `needspace`, `array`, `fancyhdr`, `emptypage`, `multicol`,
`hyperref` and `geometry`.

The fonts must be available to LuaLaTeX by filename, for example through
your TeX distribution:

| Edition | Text and Greek fonts | Mathematics font |
| --- | --- | --- |
| A5 | Cormorant Garamond, EB Garamond | Garamond Math |
| Larger | Libertinus Serif | Libertinus Math |
| Historical | Old Standard | Old Standard Math |

Latin Modern Mono is used for the license URL. Font licenses and project
links are listed in [`../RIGHTS.md`](../RIGHTS.md). Font files are not bundled.
The profiles use font filenames without machine-specific installation paths.

## Build

Run these commands from this `tex/` directory:

```sh
latexmk -lualatex -interaction=nonstopmode -halt-on-error -outdir=build/a5 sant-ilario-a5.tex
latexmk -lualatex -interaction=nonstopmode -halt-on-error -outdir=build/large sant-ilario-large.tex
latexmk -lualatex -interaction=nonstopmode -halt-on-error -outdir=build/historical sant-ilario-historical.tex
```

You can run just the command for the edition you want. `latexmk` repeats
LaTeX as needed to resolve links and the table of contents. The resulting
PDFs are in the respective `build/` subdirectories; these commands do not
replace the published PDFs in `../pdf/`. No shell escape is required.

Font and TeX versions can affect line and page breaks. A rebuilt PDF may
also differ in timestamps and other metadata even when its pages are identical.

## Edit

| File or directory | Purpose |
| --- | --- |
| `sant-ilario-*.tex` | Entry points selecting the three editions |
| `book.tex` | Shared document setup |
| `title.tex` | Title, subtitle and author |
| `source/content.tex` | Order of the book sections and back matter |
| `source/sections/` | Editable text of the preface, aphorisms, epigraphs and poems |
| `editorial-notes.tex` | German editorial notes and edition notice |
| `index.tex` | Index headwords and explicit section references |
| `shared.tex` | Common layout and semantic formatting commands |
| `profiles/` | Page geometry, fonts and type size for each edition |
| `settings.tex` | Switch for added foreign-language italics |

All three editions use the same text. The section filenames and `src:...`
labels are stable identifiers; retain the labels when editing so that index
links continue to work. Comments identifying original page ranges are kept
for reference; they do not require a scan file to build the book.

The index is supplied as editable TeX. Building resolves its existing links
automatically, but does **not** discover new terms or occurrences. Update
`index.tex` when adding or removing index references.

To disable added foreign-language italics, change `\EditorialItalicstrue` to
`\EditorialItalicsfalse` in `settings.tex` and rebuild. The editorial notice
updates to reflect the setting. Original letterspaced emphasis (`\Sperr`),
Greek text (`\Greek`) and mathematical notation (`\Math`) are independent
of this switch. Keep these semantic commands when editing passages.

## License

The [root license](../LICENSE) and [rights notice](../RIGHTS.md) apply.
The original German text remains distinct from the new editorial and
typesetting contributions. No additional license is imposed by this file.
