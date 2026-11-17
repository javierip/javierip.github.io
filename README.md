# Javier Iparraguirre >> Personal site

See the site live at [https://javierip.github.io/](https://javierip.github.io/)

Built with [MkDocs](https://www.mkdocs.org/), [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) and [mkdocs-static-i18n](https://ultrabug.github.io/mkdocs-static-i18n/).

## Setup

Create the environment once (Python 3.12):

```bash
conda create -n mkdocs-env python=3.12
conda activate mkdocs-env
pip install -r requirements.txt

# Later, to update packages
pip install --upgrade -r requirements.txt
```

On Windows, run these commands from the **Anaconda Prompt**, or run `conda init powershell` once and reopen PowerShell. If `conda` is not on your PATH, you can call the environment's Python directly:

```powershell
& "$HOME\miniconda3\envs\mkdocs-env\python.exe" -m mkdocs serve
```

## Run, build and deploy

```bash
conda activate mkdocs-env

mkdocs serve            # live preview at http://127.0.0.1:8000/
mkdocs build --strict   # build into site/ and fail on any warning (broken links, etc.)
mkdocs gh-deploy        # build and publish to the gh-pages branch
```

Run `mkdocs build --strict` before deploying to catch broken links. The `site/` folder is build output and is not committed.

The build may print a long warning about MkDocs 2 and ProperDocs (it comes from the `mkdocs-redirects` plugin). It doesn't affect the site; set `DISABLE_MKDOCS_2_WARNING=true` to hide it.

## Project layout

```text
AGENTS.md                   # Instructions for AI coding agents (CLAUDE.md imports it)
mkdocs.yml                  # Site configuration: navigation, theme, analytics, social links
requirements.txt            # Python dependencies
docs/
    index.md                # About (home page)
    leadership.md           # Leadership: how I lead teams and core competencies
    research.md             # Research: themes, publications, open-source projects
    contact.md              # Contact
    *.es.md                 # Spanish translation of each page above
    images/                 # Logo, favicon and profile photo
    stylesheets/extra.css   # Brand colors and home page components (hero, badges, cards)
```

## Editing content

- **New publication:** add it at the top of the right year in `docs/research.md` **and** `docs/research.es.md`.
- **Colors:** the palette uses `primary: custom` and `accent: custom`, so colors come from the variables at the top of `docs/stylesheets/extra.css`, not from `mkdocs.yml`.
- **Renaming or removing a page:** add a redirect under the `redirects` plugin in `mkdocs.yml` so old links keep working (for example, the old `projects.md` page now redirects to `research.md`). Spanish redirects need the full URL as the target, because the plugin can't resolve `*.es.md` pages.
- **Home page components:** the photo block (`hero`), tags (`exec-badge`) and cards (`kpi-card`) are plain HTML classes styled in `extra.css`.
- **External links:** open them in a new tab with `[text](https://...){:target="_blank"}`.
- **Don't upgrade to MkDocs 2:** it drops support for the theme and plugins used here, so keep the `mkdocs<2.0` pin in `requirements.txt`. Material for MkDocs reaches end of life on May 5, 2027; test a move to its successor (Zensical) on a separate branch first.

## Languages

The site is published in English (`/`) and Spanish (`/es/`). Each page `page.md` has a Spanish translation `page.es.md`; when you edit one, update the other. Link to pages by their English file name (for example `research.md`), even from Spanish pages; the plugin points the link to the right language. Spanish menu labels and the Spanish site description are set under the `i18n` plugin in `mkdocs.yml`.
