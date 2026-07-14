# StARLinG Lab — Redesigned Site (Deploy Package)

## What's in here
47 self-contained HTML pages (the full redesigned site: homepage, People, Publications,
Projects + 27 project detail pages, Software, Datasets + 13 dataset detail pages, Gallery,
News archive) plus `assets/` (images, headshots, PDFs, sponsor logos) and `data/` (the
publications dataset, loaded at runtime by Publications.html).

`index.html` is the homepage.

## How to deploy to starling-lab.github.io

1. In your `starling-lab.github.io` repo, **back up or remove** the old Jekyll site files
   you're replacing (the `_pages`, `_posts`, `_projects`, `_data` Jekyll source — GitHub
   Pages will otherwise still try to build the old Jekyll site on top of this).
2. Copy every file from this package into the **repository root**, preserving the folder
   structure (`index.html`, `People.html`, ..., `assets/`, `data/` all at the root).
3. Add an empty file named `.nojekyll` at the repo root. This tells GitHub Pages to serve
   the files as-is instead of running them through Jekyll (important — Jekyll would try to
   process these and can break things).
4. Commit and push to the branch your GitHub Pages is configured to serve from (usually
   `main` or `gh-pages`).
5. Visit `https://starling-lab.github.io/` after a minute or two to confirm it's live.

## Notes
- All internal navigation links point to plain `.html` files (e.g. `People.html`), matching
  the filenames in this package — don't rename them, or update links to match.
- Every page is a single, self-contained HTML file (fonts/styles inlined) except for images
  and PDFs, which load from the sibling `assets/` folder, and `Publications.html`, which
  loads `data/publications-data.js` for its paper list. Keep `assets/` and `data/` alongside
  the HTML files.
- External links (GitHub repos, arXiv, YouTube, dataset zip downloads) point to their real
  live URLs and need no changes.
- If you'd rather keep the site on Jekyll long-term, treat this package as the visual/content
  reference and have a developer port it into your existing Jekyll templates instead of using
  these files directly.
