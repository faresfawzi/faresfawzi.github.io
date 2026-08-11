# faresfawzi.github.io

Personal academic website for [Fares Fawzi](https://faresfawzi.github.io), built with [Jekyll](https://jekyllrb.com/) and the [al-folio](https://github.com/alshedivat/al-folio) theme, hosted on GitHub Pages.

---

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) — for local development
- [Node.js / npm](https://nodejs.org/) — for running Prettier before commits
- Git

Install Prettier (one-time setup):

```bash
npm install --save-dev prettier @shopify/prettier-plugin-liquid
```

---

## Local Development

```bash
# Start the local server
docker compose pull && docker compose up

# Site runs at http://localhost:8080
# LiveReload at http://localhost:35729
```

```bash
# Rebuild after changing Gemfile or Dockerfile
docker compose up --build

# Stop the server
docker compose down
```

> **Note:** Changes to `_config.yml` require a full restart (`docker compose down && docker compose up`) — they are not picked up by the file watcher.

---

## File Structure

Only the files you actively edit are listed here.

```
faresfawzi.github.io/
│
├── _config.yml                  # Main site config: name, URL, socials toggle, theme settings
│
├── _data/
│   ├── socials.yml              # Social links (email, Scholar, LinkedIn, CV)
│   └── coauthors.yml           # Coauthor URLs (auto-links author names in publications)
│
├── _pages/
│   ├── about.md                 # Home page (/) — bio, research interests, news
│   ├── about_me.md              # About tab (/about/) — education, experience, fellowships
│   ├── publications.md          # Publications tab (/publications/)
│   ├── cv.md                    # CV tab (/cv/) — embeds the PDF
│   ├── blog.md                  # Blog tab (currently unpublished)
│   └── news.md                  # Full news page (/news/)
│
├── _news/                       # News items shown on home page
│   ├── 2026-07-06-icml.md
│   ├── 2026-06-29-refine-aied.md
│   ├── 2026-06-27-festival-of-learning.md
│   ├── 2026-01-01-aied.md
│   ├── 2025-10-01-emnlp.md
│   └── 2024-09-01-phd-start.md
│
├── _bibliography/
│   └── papers.bib               # All publications in BibTeX format
│
├── assets/
│   ├── img/
│   │   ├── headshot.jpg         # Profile photo (used on home page)
│   │   ├── favicon.png          # Browser tab icon
│   │   ├── logos/               # Institution and brand logos
│   │   │   ├── epfl.png
│   │   │   ├── ucl.png
│   │   │   └── informedai.png
│   │   └── publication_preview/ # Thumbnail images for publications
│   │       ├── refine.png
│   │       └── scribe.png
│   └── pdf/                     # PDF files (not the CV — see below)
│
├── fares_CV_2026-2.pdf          # CV PDF served at /fares_CV_2026-2.pdf
│
└── .github/workflows/
    └── deploy.yml               # GitHub Actions: builds and deploys to GitHub Pages
```

---

## Adding a News Item

Create a file in `_news/` named `YYYY-MM-DD-slug.md`.

**Plain text item (no link):**

```markdown
---
layout: post
date: 2026-07-06
inline: true
---

🇰🇷 Attending ICML 2026 in Seoul, Korea (July 6–11).
```

**Linked item (links to a page):**

```markdown
---
layout: post
title: "🎉 REFINE accepted at AIED 2026"
date: 2026-03-01
link: /publications/#fawzi2026refine
---
```

---

## Adding a Publication

Add a BibTeX entry to `_bibliography/papers.bib`. Supported fields:

```bibtex
@inproceedings{key,
  title     = {Paper Title},
  author    = {Last, First and Last, First},
  booktitle = {Conference Name},
  year      = {2026},
  month     = mar,
  note      = {Full paper (oral)},       % shown as a subtitle line
  pdf       = {https://...},             % PDF button + title link
  url       = {https://...},             % fallback title link
  doi       = {10.xxxx/...},             % DOI button
  arxiv     = {2603.29142},              % arXiv button
  abstract  = {Paper abstract text.},    % enables Abstract toggle button
  preview   = {filename.png},            % thumbnail (put file in assets/img/publication_preview/)
}
```

The title links to `pdf` if set, then `url`, then `doi`, then `arxiv`.
The `abstract` field adds an **Abstract** button that expands inline.

---

## Pushing to GitHub Pages

**Before every push**, format all files with Prettier:

```bash
npx prettier . --write
```

Then commit and push:

```bash
git add -A
git commit -m "Your message"
git push origin main
```


GitHub Actions automatically builds and deploys the site. Monitor progress at:
**https://github.com/faresfawzi/faresfawzi.github.io/actions**

The live site updates at **https://faresfawzi.github.io** within ~2 minutes.

---

## Updating the CV

1. Replace `fares_CV_2026-2.pdf` in the repo root with the new file
2. If the filename changes, update `_data/socials.yml` (`cv_pdf` field) and `_pages/cv.md`

---

## Theme

Built on [al-folio](https://github.com/alshedivat/al-folio). For advanced customisation see the [al-folio docs](https://github.com/alshedivat/al-folio/blob/master/CUSTOMIZE.md).
