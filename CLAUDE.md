# CLAUDE.md — Astro Paper Wiki

Read this whole file before doing anything in this project.
These rules apply every time, even if the request is short.

---

## 1. What this project is

A personal research wiki of astrophysics papers, published as a website on GitHub Pages.

- **Who it's for:** me — a CS student taking an astrophysics seminar. I understand
  code and math, but NOT astrophysics jargon.
- **Goal:** every paper I read is broken into reusable knowledge. Papers link to
  concepts, concepts link back to every paper that uses them. Over time the
  concept pages collect evidence from many papers.
- **Not the goal:** a list of summaries. If a new paper doesn't connect to any
  existing concept, that is still fine, but always look for connections first.

This follows the LLM Wiki pattern (raw → wiki → rules):

| Layer | Folder / file | Who edits it |
|---|---|---|
| raw sources | `raw/sources.md` (links to the original papers) | me — never change the paper info |
| wiki | `papers/`, `concepts/`, `index.html` | the AI writes and maintains these |
| rules | `CLAUDE.md` (this file) | me and the AI, together |

---

## 2. Folder structure

```
index.html                 home page (hero, paper cards, concept index)
style.css                  the ONLY stylesheet, shared by every page
papers/                    one html file per paper
concepts/                  one html file per concept
templates/
  paper-template.html      copy this to make a new paper page
  concept-template.html    copy this to make a new concept page
raw/sources.md             list of original papers (arXiv links)
wiki-index.md              catalog of every page, one line each (read this FIRST)
log.md                     history of every change, newest at the bottom
CLAUDE.md                  this file
README.md                  short public intro to the project
.nojekyll                  empty file, tells GitHub Pages to skip Jekyll (never delete)
.gitignore                 keeps Mac's .DS_Store files out of the repo
```

Do not create any other folders without asking me.

---

## 3. File naming

- Lowercase English letters, numbers and hyphens only. No spaces, no Chinese,
  no capital letters. (GitHub Pages is case-sensitive.)
- **Paper:** `papers/<year>-<first-author-surname>-<2-to-4-word-topic>.html`
  e.g. `papers/2026-caddy-moonlit-satellites.html`
  - `<year>` = year of the arXiv ID (2609.xxxxx → 2026)
- **Concept:** `concepts/<concept-name>.html`, singular noun, no abbreviations
  unless the abbreviation is the common name.
  e.g. `concepts/dark-energy.html`, `concepts/brdf.html`
- All links between pages are **relative** (`../concepts/moon.html`), never
  absolute `https://` links to my own site.

---

## 4. Visual style — "space dark, gradient, bold but clean"

Use only `style.css`. Never add inline `style=""` attributes or new css files.
Never change these values unless I ask:

| Token | Value | Use |
|---|---|---|
| `--bg` | `#06081A` | page background (deep space navy) |
| `--surface` | `#0E1330` | cards, tables |
| `--line` | `#232A55` | borders |
| `--text` | `#EEF1FF` | main text |
| `--muted` | `#98A1C8` | secondary text |
| `--g1` → `--g2` → `--g3` | `#4F6BFF` → `#B04BFF` → `#FF7A59` | the signature gradient (blue → violet → orange) |
| `--warn` | `#FFC857` | "to verify" notes |

- **Fonts:** `Space Grotesk` (headings, bold), `Inter` (body), `JetBrains Mono`
  (numbers, IDs, code). Loaded from Google Fonts in each page's `<head>`.
- **Gradient use:** big blurred gradient "orbs" in the background, gradient text
  for the main title only, gradient top-edge on cards. Body text is never a gradient.
- **Clean:** lots of space, max content width 1080px, rounded corners 18px,
  no drop-shadow clutter, no emoji in headings.
- **Field tags** (colored chips on paper cards): `observational`, `theory`,
  `instrumentation`, `cosmology`, `satellites`, `planetary`. Add a new tag only if
  none fit, and add it to this list. A tag without its own color in `style.css`
  uses the default blue chip, which is fine.

---

## 5. Paper page template (`templates/paper-template.html`)

Every paper page has exactly these sections, in this order:

1. **Header** — title, authors (`First Author et al.`), arXiv ID + link, field tags
2. **TL;DR** — ONE sentence a CS student can understand
3. **Research question** — what they wanted to find out (2–3 sentences)
4. **Data & tools** — telescopes, instruments, datasets, software (bullet list)
5. **Method** — numbered steps, max 6
6. **Key results** — table: `Result | Value | Where in paper` (section / figure / table)
7. **Conclusions** — max 4 bullets
8. **Limitations** — max 5 bullets
9. **⚠ To verify** — anything inconsistent or unclear in the paper (can be empty: write "nothing flagged")
10. **Concepts in this paper** — chips linking to each concept page
11. **My seminar questions** — 3 questions I could ask the presenter
12. **Footer** — back to home, "added on YYYY-MM-DD"

---

## 6. Concept page template (`templates/concept-template.html`)

1. **Header** — concept name, one-line definition
2. **Plain explanation** — 3–6 sentences for a CS student, with ONE everyday analogy
3. **Why astronomers care** — 2–3 bullets
4. **Appears in** — one row per paper: paper link + how THAT paper uses this concept
5. **⚠ Conflicting findings** — only if two papers disagree; otherwise omit the section
6. **Related concepts** — chips linking to other concept pages
7. **Footer** — back to home

---

## 7. How to add a new paper ("ingest") — follow every step

When I say *"ingest this paper: <link or pdf>"*:

1. Read `wiki-index.md` first so you know which pages already exist.
2. Read the paper. Add it to `raw/sources.md` (title, authors, arXiv link).
3. Create `papers/<file>.html` by copying `templates/paper-template.html`.
   Fill every section from section 5. Cite the section/figure/table for each number.
4. List the paper's 4–8 most important concepts. For each one:
   - **already exists** in `wiki-index.md` → open that concept page and ADD a row
     to "Appears in". Do not rewrite the existing explanation.
   - **doesn't exist** → create it from `templates/concept-template.html`.
   - if this paper **disagrees** with a paper already listed → add/extend the
     "⚠ Conflicting findings" section on that concept page. Only for real
     disagreements about the SAME thing (same object, same quantity). Two papers
     explaining different objects in different ways is not a conflict; just add
     both rows to "Appears in".
5. Update `index.html`:
   - add a paper card to the papers grid, sorted by arXiv ID, newest first
     (2609.xxxxx before 2605.xxxxx). Order is by publication, NOT by date added.
   - add new concepts to the concept index (keep A–Z order)
   - update the counters (papers / concepts)
6. Update `wiki-index.md` (one line per new page) and add one line to `log.md`:
   `YYYY-MM-DD | ingest | <paper file> | +N concepts, ~M concepts updated`
7. Run the done-check (section 10) and report it to me.

When I give several papers at once: ingest them ONE AT A TIME in arXiv-ID order
(oldest first), doing all 7 steps for each before starting the next, with one
`log.md` line per paper. That way a later paper can reuse concepts an earlier one created.

Other commands I may use:
- *"lint"* → check every page: broken links, concepts with no papers,
  papers with no concepts, missing sections, files that break section 3.
  Report the problems, fix only after I say yes, then log it.
- *"explain <concept>"* → answer using ONLY the wiki pages, and say which pages you used.

---

## 8. Writing rules

- Write in clear English. Explain jargon the first time it appears on a page.
- **Never invent numbers, results or citations.** Every number must come from the
  paper and show where (e.g. "Sec. 3.1", "Table 2", "Fig. 12").
- If the paper is unclear or contradicts itself → put it in "⚠ To verify",
  don't guess which version is right.
- Don't copy long sentences from the paper. Summarize in your own words;
  short quotes (under 15 words) only for definitions, in quotation marks.
- Concept pages must make sense to someone with zero astrophysics background.

---

## 9. Code comments (my personal style)

When writing or changing html / css / js, add short comments ONLY on the
tricky or easy-to-forget parts — as if I'm leaving notes for future me.

- all lowercase, casual, human words, one line
- explain *why*, not *what*
- no comments on obvious stuff (no "this is the header")

Good: `/* the grain overlay needs pointer-events none or it eats every click */`
Bad:  `/* Header Section Styles */`

---

## 10. Done-check (report this after every change)

- [ ] new/changed pages follow the template order exactly (section 5 / 6)
- [ ] file names follow section 3
- [ ] every link works: home ↔ paper ↔ concept, and "back to home" on every page
- [ ] every number has a "where in paper" reference
- [ ] `index.html` counters and cards are updated
- [ ] `wiki-index.md` and `log.md` are updated

Then tell me: files created, files changed, anything flagged "to verify".

---

## 11. Never do this

- Never delete a page or a row from "Appears in" — ask me first.
- Never change colors, fonts or layout (section 4) without asking.
- Never upload paper PDFs to this repo — link to arXiv instead (copyright).
- Never put API keys, passwords or personal info anywhere (the repo is public).
- Never use frameworks or build tools — plain html + css only, so GitHub Pages
  works with zero setup.
- Never delete `.nojekyll`. Without it GitHub Pages runs Jekyll on the repo and
  the site can fail to build (this happened once, the site showed a 404).

---

## 12. Rule change log

When something goes wrong, add a rule above and note it here.

- 2026-11-15 — first version.
- 2026-11-16 — site showed 404 after publishing → added `.nojekyll` + rule in section 11.
- 2026-11-16 — while ingesting paper 3, "add card at the TOP (newest first)" was
  ambiguous (newest published or newest added?) → section 7 now says sort by arXiv ID.
- 2026-11-16 — paper 3 (planetary science) fit no field tag → added `planetary` to section 4.
- 2026-11-16 — got 4 papers at once with no rule for batches → section 7 now says one
  at a time in arXiv order, so later papers can reuse concepts from earlier ones.
- 2026-11-16 — two ultracool dwarf papers explained odd spectra differently (dust vs
  aurora) but about different objects → section 7 now defines what counts as a conflict.
