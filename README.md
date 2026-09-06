# Research blog — Quarto project

## One-time setup

1. Install Quarto: <https://quarto.org/docs/get-started/> (there's an installer
   for macOS, Windows and Linux — no command line needed for this step).
2. If you want code chunks to run at render time, you also need Python with
   `jupyter`, `matplotlib` and whatever your posts import:
   `pip install jupyter matplotlib numpy`.

## Day to day

```bash
quarto preview     # live preview at localhost:4000, reloads as you save
quarto render      # builds the finished site into _site/
```

## Publishing

The simplest route is GitHub Pages:

```bash
git init && git add . && git commit -m "first post"
# create an empty repo on GitHub, then:
git remote add origin git@github.com:yourhandle/blog.git
git push -u origin main
quarto publish gh-pages
```

Netlify works too (`quarto publish netlify`) and gives you a custom domain
more easily. Either way the output is plain static files — nothing to run, no
server to maintain.

## Adding a post

Make a dated folder and an `index.qmd` inside it:

```
writing/2026-09-14-my-new-note/index.qmd
insights/2026-09-14-a-short-one/index.qmd
```

Anything in `writing/` shows up on the Scientific writing page; anything in
`insights/` shows up on Tech insights. The listings pick up the front matter
automatically — no index to maintain.

Minimum front matter:

```yaml
---
title: "Your title"
description: "One sentence — this is what shows in the listing."
date: 2026-09-14
categories: [interpretability, method]
---
```

Useful extras: `image: figure-1.png` gives the listing a thumbnail;
`draft: true` keeps a post out of the listings until you're ready.

## What goes where

| File | What it does |
|---|---|
| `_quarto.yml` | Site config: nav, footer, format defaults, bibliography |
| `styles.scss` | All the design — palette, type, listing and code styling |
| `index.qmd` | Home page: hero, feature grid, four most recent posts |
| `about.qmd` | About + links to your other platforms |
| `writing.qmd` | Auto-generated listing of `writing/` |
| `insights.qmd` | Auto-generated grid listing of `insights/` |
| `includes/feature-grid.html` | The signature grid. Edit the `features` array as you publish |
| `references.bib` | Citations — cite with `[@key]` in any post |

## Notes

- Math works out of the box: `$inline$` and `$$display$$`.
- To publish a Jupyter notebook as a post, drop the `.ipynb` in a dated folder
  instead of an `index.qmd` — Quarto renders it directly.
- `execute: freeze: auto` in `_quarto.yml` means a post's code runs once and is
  cached, so rebuilds stay fast. Delete `.quarto/` to force a re-run.
- Replace every `example.com` / `yourhandle` placeholder before publishing.
