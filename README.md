# Research Updates

A LaTeX repository for chronological research updates, organized by month.

The `research_update` command creates the current monthly file if needed, adds today's heading if needed, and opens the file in Vim.
The complete document is compiled from `main.tex`.

## Quick start

1. Create a repository from this template and clone it.
2. Edit the personal details and current-project list in `main.tex`.
3. Optional: Replace or omit the cover image `images/Grothendieck-Riemann-Roch.jpg`.
4. Install the command as described below, or run it directly:

   ```bash
   bash scripts/research_update
   ```

5. Compile from the repository root:

   ```bash
   latexmk -pdf main.tex
   ```

Requirements: Bash, Vim, a TeX installation containing the packages used
in `main.tex`, Latexmk and Biber.

## Repository structure

```text
research-diary/
├── .gitignore
├── README.md
├── main.tex
├── refs.bib
├── images/
│   └── Grothendieck-Riemann-Roch.jpg
├── scripts/
│   └── research_update
└── months/
    ├── 2026-11.tex
    ├── 2026-12.tex
    └── ...
```

- `main.tex`: preamble, cover, project list, contents and monthly includes.
- `refs.bib`: bibliography database.
- `images/`: cover image and any other figures.
- `scripts/research_update`: command for starting an update.
- `months/`: monthly files, created automatically when needed. The filenames above are examples; this folder is initially absent and created automatically by `research_update`.

## Installing the command

From the repository root:

```bash
chmod +x scripts/research_update
mkdir -p "${HOME}/.local/bin"

ln -s "$(pwd -P)/scripts/research_update" "${HOME}/.local/bin/research_update"
```

Optionally, also install the shorter command `uu`:

```
ln -s "$(pwd -P)/scripts/research_update" "${HOME}/.local/bin/uu"
```

Ensure `~/.local/bin` is in your `PATH`. If necessary, add this line to
your shell configuration and run it in your current terminal:

```bash
export PATH="${HOME}/.local/bin:${PATH}"
```

Check the installation:

```bash
command -v research_update
command -v uu
```

Both commands work from any directory and open the repository to which
their symlinks point. Keep that repository at the symlink target, or
recreate the links after moving it.

To uninstall:

```bash
rm "${HOME}/.local/bin/research_update"
rm "${HOME}/.local/bin/uu"
```

## Writing updates

Run `research_update` or `uu`. Repeated runs on the same day do not
duplicate the daily heading.

Write ordinary LaTeX below the heading. Use

```latex
\ptag{p1}
```

to mark the current topic of discussion, in this case project P1.
Optional project shortcuts can be configured using the commented examples
in the preamble. For example, `\newcommand{\myproject}{\ptag{TAG}}` lets you use `\myproject`
in the project list and daily entries. An example with optional decoration is also included.

Use

```latex
\astbreak
```

to insert a separator, e.g. to start a new topic of discussion when it does not have a project tag.

The `\arxiv` command takes as input the numeric part `YYMM.NNNNN` of the [arXiv identifier](https://info.arxiv.org/help/arxiv_identifier.html)
of a paper `arXiv:YYMM.NNNNN` and includes a link to that arXiv paper with link text `arXiv:YYMM.NNNNN`.

The color of daily headings is set once in
`main.tex`:

```latex
\definecolor{DateColor}{RGB}{0,128,128}
```

Vim opens with `months/` as its working directory. Your shell's working
directory is unchanged when Vim closes.

## Numbering and references

Theorem-like environments share a counter that restarts at 1 each month.
Equations have a separate counter that also restarts each month.
Printed numbers omit the chapter number.

Use unique LaTeX labels throughout the document. When referring across
months, mention the date if necessary to distinguish repeated numbers.

Every day receives a label of the form `day:YYYY-MM-DD`:

```latex
See \hyperref[day:2026-11-04]{the update from November 4}.
```

These day labels are hyperlink targets rather than numbered references.

## Monthly files and compilation

The `research_update` command manages monthly `\include` statements in `main.tex`.
Keep the `% Monthly files:` marker and the monthly `\chapter{...}` commands.

Compile `main.tex`, not the individual monthly files:

```bash
latexmk -pdf main.tex
```

Add bibliography entries to `refs.bib`; the document uses BibLaTeX
with Biber.

## AI disclaimer

AI's assistance has been used to update the code in this repository.
Every line of code suggested by AI used in the code of this repository
was carefully reviewed by a human.
