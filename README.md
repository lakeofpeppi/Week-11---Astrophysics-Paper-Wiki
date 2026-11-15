# Astro Paper Wiki

A personal research wiki of astrophysics papers, explained for a CS student.
Each paper is broken into reusable **concept pages**. Papers link to concepts,
and every concept collects all the papers that use it, so the wiki gets more
connected with every paper added.

**Live site:** https://lakeofpeppi.github.io/Week-11---Astrophysics-Paper-Wiki/

## How it works

The AI maintains this site by following [`CLAUDE.md`](CLAUDE.md), the project's
rulebook. To add a paper I only say:

> Read CLAUDE.md. Ingest this paper: https://arxiv.org/abs/xxxx.xxxxx

and the rules tell the AI to create the paper page from the template, update or
create concept pages, update the home page, `wiki-index.md` and `log.md`, then
report a done-check.

## Structure

| Path | What |
|---|---|
| `CLAUDE.md` | rules: purpose, style, templates, ingest steps, don'ts |
| `index.html` | home page |
| `papers/` · `concepts/` | wiki pages |
| `templates/` | page templates the AI copies |
| `wiki-index.md` | catalog of all pages (the AI reads this first) |
| `log.md` | history of changes |
| `raw/sources.md` | links to the original papers |

Plain HTML + CSS, no build step. Hosted on GitHub Pages.
