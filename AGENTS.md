# AGENTS.md

## PLAN AND ASK BEFORE DO

**CRITICAL: NEVER EVER DO ANY ACTION READING, MODIFYING OR RUNNING without explaining the plan.**

Each set of intended actions needs to be explained in the format:

> I understood that `<YOUR ANALYSIS>` so that I plan to `<GOALS YOU PURSUE>` by `<ACTIONS TO BE CONFIRMED>` estimating `<# of ITEMS>` `<ITEMS>` to be worked on. Confirm with go!

**YOU WILL NEVER PROCEED WITHOUT POSITIVE CONFIRMATION by go!**

## Efficiency

- Do NOT do unneeded file lookups based on guessing or assuming typos.
- Do NOT use TodoWrite for tasks with fewer than 4 steps.
- Do NOT read files you already have contents for.
- Keep summaries to 2-3 lines max unless asked for detail.

## CR Wiki

The cr wiki is at https://cr.bitplan.com
Use `wikiupload --files <file> -t cr` to upload files.
Use the wikipush_* tools to read/edit wiki pages.
- Minimize tool calls. Batch parallel calls. Avoid redundant calls.

## Security

**CRITICAL: NEVER leak credentials, passwords, hashes, internal hostnames, IPs, or any infrastructure details to public platforms (GitHub, Discourse, etc.). Firing offense.**

## Scientific Paper

This project is a scientific paper. AI support is strictly limited to:

- **Corrections**: spelling and grammar errors
- **Tool support**: creating tables, graphics, and similar formatting tasks

AI must NOT generate, rewrite, or contribute original scientific content, arguments, or prose.

## GitHub Automation

This project uses GitHub Actions to automatically build the PDF from LaTeX sources on every push to `main`.

### Structure

- `.github/workflows/build.yml` — CI workflow: checks out repo, builds PDF via `scripts/tex2pdf --github`, and commits the updated PDF if changed
- `scripts/tex2pdf` — LaTeX build script (pdfLaTeX + BibTeX, 3-pass). Supports `--build`, `--check`, `--install`, `--clean`, `--fonts`, `--github`, and `--help`
- `scripts/bash_messages` — Colored terminal messaging helper (sourced by `tex2pdf`)
- `.gitignore` — Excludes LaTeX build artifacts
- `README.md` — Links to the PDF in the repo

### CI Workflow

On push to `main`, the GitHub Action:
1. Checks out the repository
2. Runs `scripts/tex2pdf --github` inside a `texlive/texlive:latest` container
3. If the PDF changed, commits with `build: auto-update PDF [skip ci]`
4. Pushes the commit

Reference: adapted from [ScholiaGraphSplitPaper](https://github.com/WolfgangFahl/ScholiaGraphSplitPaper).
