# pipekit.dev

The discovery surface for [pipekit](https://github.com/altack/pipekit) recipes — a static site listing every recipe in [`altack/pipekit-recipes`](https://github.com/altack/pipekit-recipes) plus any community publishers registered there.

## How it works

1. The indexer in `altack/pipekit-recipes` walks `recipes/**/recipe.yaml` and the publishers listed in `publishers.yaml`, then writes a single `index.json` to that repo's `gh-pages` branch.
2. This site is one self-contained `index.html` that fetches `https://altack.github.io/pipekit-recipes/index.json` at page-load and renders cards + detail views client-side.
3. There is no build step. Open `index.html` locally to develop; deploy by pushing to the `main` branch (GitHub Pages serves from `/` of `main`).

When the recipe set or output shape grows beyond what one HTML file can carry, this becomes an Astro project. Until then, simplicity wins.

## Deploy

GitHub Pages serves `main:/` directly. Pushing to `main` is the deploy.

A custom `pipekit.dev` CNAME can be added later — drop a `CNAME` file containing `pipekit.dev` and configure DNS at the registrar.

## Local development

```bash
# any static file server works
python3 -m http.server 8000
# or
bunx serve .
```

Then open <http://localhost:8000>.

## What this repo is *not*

- Not a backend. There is no server-side code.
- Not a content store. Every recipe in this site lives in `altack/pipekit-recipes` (or a registered publisher's repo).
- Not the runtime. The runner image is at `altack/pipekit`.
