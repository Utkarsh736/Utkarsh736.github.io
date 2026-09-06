# Utkarsh736 — Portfolio

A fresh, light, clear portfolio built with [Quarto](https://quarto.org). Light "paper" theme with a teal accent, automatic dark mode, and a workflow that stays entirely in Markdown.

Live site: <https://utkarsh736.github.io/>

## How the site is organised

```text
_quarto.yml            Site config: pages, navbar, footer, theme, colors
theme-light.scss       Light theme design tokens (colors, fonts, radii)
theme-dark.scss        Dark theme design tokens (auto-paired toggle)
styles.css             All component styling (hero, cards, chips, timeline...)
index.qmd              Homepage: hero + featured apps + latest writing
about.qmd              Bio, skills, experience timeline, contact block
blogs/
  blogs.qmd            Blog listing page (renders automatically)
  posts/               Drop .qmd or .ipynb files here — done, they're live
apps/
  apps.qmd             Apps grid page (renders automatically)
  posts/               One .qmd per app (Bearify, Docker demo)
_templates/            Copy-paste starting points (ignored by Quarto)
assets/                Images, resume, thumbnails (kept out of git — see below)
docs/                  Rendered site (this is what GitHub Pages serves)
.github/workflows/     Optional CI publish workflow
```

## Everyday edits

**Update the bio / role / experience** — edit `about.qmd`. The bio is plain
paragraphs; jobs are entries inside the `.timeline` block; skill chips are
single words in `[brackets]{.chip}`. Text only, no HTML needed.

**Publish a blog post** — copy `_templates/blog-post-template.qmd` into
`blogs/posts/`, rename it, fill in the title/date/description, write your post,
run `quarto render`, commit. New posts appear on the Blogs page and in the
homepage "Latest Writing" list automatically.

**Publish an app** — copy `_templates/app-post-template.qmd` into
`apps/posts/`, swap in your Hugging Face Space URL in the iframe, add a
thumbnail under `assets/`. It joins the Apps grid and the homepage "Featured
Apps" section on its own.

**Change the accent color / fonts** — open `theme-light.scss` and
`theme-dark.scss`. Every color is a small set of variables at the top plus the
matching `--token` list below it (e.g. change all `#0d9488` to your new hue).
Component styling in `styles.css` only references those tokens, so a palette
swap touches two files and nothing else.

**Add a link everywhere at once** — the social chips are plain HTML anchors
repeated in `index.qmd` and `about.qmd`; search for `chip-link` and edit the
URLs.

## Running locally

1. Install Quarto: <https://quarto.org/docs/get-started/>
2. From the repo root: `quarto preview` — opens the site with live reload.

## Publishing

The rendered site lives in `docs/` and GitHub Pages serves it from the `main`
branch. After making changes:

```bash
quarto render
git add .
git commit -m "update site"
git push
```

A `Quarto Publish` GitHub Actions workflow is also included: if you prefer
CI-based publishing, switch the repo's Pages source to the `gh-pages` branch
(Settings → Pages) and the workflow takes over on every push.

> **Note on `assets/`:** this folder is listed in `.gitignore`, so your photo,
> thumbnails, and resume are NOT pushed to the public repo. The committed
> `docs/` folder is what visitors see. If you ever switch to CI-only
> publishing, remove `/assets/` from `.gitignore` so the render can find your
> images — and keep `assets/Resources/resume.pdf` in mind when linking your CV
> from the About page.

## License

[MIT](LICENSE)
