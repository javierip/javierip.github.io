# Agent instructions

Personal site of Javier Iparraguirre, published at <https://javierip.github.io/>. Static site built with MkDocs 1.6 + Material for MkDocs, in English and Spanish.

## Audience and tone

The site serves **two audiences at once**: academics (researchers, students, collaborators) and industry (executives, recruiters, engineering leaders).

- Write plainly and factually. Executive framing belongs mainly on the Leadership page; keep the home page balanced.
- **Never invent or inflate claims.** No made-up metrics (e.g. "10x–50x cheaper"), titles, patents, awards, or "proprietary" labels for open-source work. Only state results that are published (see `docs/research.md`) or that the owner provided.
- Don't mention unpublished projects or methods unless the owner says they're public.
- Use "Professor" for the UTN role (not "Adjunct Professor"; in Argentina "Profesor Adjunto" is a different rank).

## Build and verify

The Python environment is the conda env `mkdocs-env`. `conda` is usually **not** on the PATH of agent shells, so call its Python directly:

```bash
# Git Bash
DISABLE_MKDOCS_2_WARNING=true /c/Users/jipar/miniconda3/envs/mkdocs-env/python.exe -m mkdocs build --strict
```

```powershell
# PowerShell
$env:DISABLE_MKDOCS_2_WARNING = "true"; & "$HOME\miniconda3\envs\mkdocs-env\python.exe" -m mkdocs build --strict
```

- `mkdocs build --strict` must pass with no warnings before you report a change as done.
- `site/` is build output (gitignored). Don't edit or commit it.
- If you install a dependency, add it to `requirements.txt` too.
- **Do not upgrade to MkDocs 2.** It drops support for the theme and plugins used here; keep the `mkdocs<2.0` pin. Material for MkDocs reaches end of life on May 5, 2027; a move to its successor (Zensical) should be tested on a separate branch first.

## Structure

| File | Purpose |
| :--- | :--- |
| `mkdocs.yml` | Navigation, theme, plugins (search, i18n, redirects), analytics, social links |
| `docs/index.md` | About (home): hero with photo and badges, focus-area cards, education |
| `docs/leadership.md` | How he leads, core competencies table |
| `docs/research.md` | Research themes, full publication list, open-source projects |
| `docs/contact.md` | Email, topics, profiles |
| `docs/*.es.md` | Spanish version of each page |
| `docs/stylesheets/extra.css` | All custom colors and components |
| `docs/images/` | Logo, favicon, profile photo |

## Bilingual rules (mkdocs-static-i18n, suffix structure)

- **Every content change must be made in both `page.md` and `page.es.md`.** Keep them structurally identical (same sections, same links).
- Link to pages by their **English file name** (`research.md`), even from Spanish pages; the plugin resolves the language.
- Spanish menu labels go in `nav_translations` in `mkdocs.yml`; the Spanish `site_description` is set there too.
- Spanish style: decimal comma and spaced units (`3,4 M`, `5,1 puntos`); the site uses Argentine *voseo* ("podés").

## Content conventions

- Open external links in a new tab: `[text](https://...){:target="_blank"}`.
- New publication: add it at the top of the right year in `docs/research.md` and `docs/research.es.md`, following the existing format (bold title, authors, italic venue line, links separated by ` · `).
- Pages hide the left navigation via front matter (`hide: [navigation]`); the home and contact pages also hide the table of contents.
- These identifiers are correct; don't change them unless the owner asks: email `j.iparraguirre@computer.org`, LinkedIn `/in/jiparraguirre/`, Google Scholar user `PNNFrAQAAAAJ`, GitHub `javierip`, X `javieripa`, analytics `G-8ZT4TE5E92`.

## Styling

- The palette uses `primary: custom` and `accent: custom`, so **all colors live in `docs/stylesheets/extra.css`**, not in `mkdocs.yml`.
- Light-mode tokens are declared on `:root, [data-md-color-scheme="default"]`. The second selector is required: Material sets the link color on it, and `:root` alone loses (links turned black). Dark-mode tokens are on `[data-md-color-scheme="slate"]`.
- Material colors links and outlined buttons with the header color by default, which is invisible in dark mode. Keep `--md-typeset-a-color` and the `.md-button` rules in `extra.css`.
- Light mode is the default (first palette entry). Check **both** light and dark mode, and a narrow (phone) width, after any visual change.
- To check visually without a browser session: build to a scratch folder and screenshot with headless Edge (`msedge --headless=new --screenshot=out.png --window-size=1400,1500 file:///.../index.html`). For dark mode, build from a copy of `mkdocs.yml` with the light palette entry removed. Headless Edge can't go narrower than about 500 px, so use 600 px for the phone check.

## Renaming or removing pages

Add a redirect under the `redirects` plugin in `mkdocs.yml` so old URLs keep working. Spanish targets must be full URLs (e.g. `es/projects.md: https://javierip.github.io/es/research/`) because the plugin can't resolve `*.es.md` pages.

## Git and deployment

- Work on the `dev` branch; `main` is the base for pull requests.
- Don't commit, push, or run `mkdocs gh-deploy` unless the owner asks. Deploying publishes the live site.
