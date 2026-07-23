# Lihao's Personal Website

Jekyll site (Minimal Mistakes) hosted on GitHub Pages: [yanlihao.com](https://yanlihao.com).

## Local preview (WSL recommended)

From the repo root in WSL:

```bash
export PATH="$HOME/gems/bin:$PATH"
export GEM_HOME="$HOME/gems"
cd /mnt/c/Users/shida/github/liaoliao-24.github.io

bundle install   # first time, or after Gemfile changes
bundle exec jekyll serve --host 0.0.0.0 --port 4000 --livereload
```

Then open [http://localhost:4000](http://localhost:4000).

If a port is busy:

```bash
fuser -k 4000/tcp 35729/tcp
```

`_site/` is the generated output. It is gitignored — do not commit it. If it was tracked before:

```bash
git rm -r --cached _site
```

## Site layout

| Path | Purpose |
|------|---------|
| `_posts/` | Blog posts (dated Markdown files) |
| `_pages/` | Standalone pages (Home, Life, Society, etc.) |
| `_data/navigation.yml` | Top navigation tabs |
| `assets/images/` | Images (prefer a folder per category) |
| `_config.yml` | Site-wide settings (title, theme, URL, etc.) |

Categories used for tabs: `computational-neuroscience`, `society`, `life`.

## Add a post

1. Put images under `assets/images/<category>/` (e.g. `assets/images/life/`).
2. Create `_posts/YYYY-MM-DD-short-slug.md`:

```markdown
---
title: "Your Title"
categories:
  - life
tags:
  - life
header:
  teaser: /assets/images/life/your-teaser.png
---

Short intro paragraph.

![Alt text](/assets/images/life/your-teaser.png)
```

3. Filename date controls sort order; `categories` must match a tab taxonomy (`life`, `society`, or `computational-neuroscience`) for the post to appear on that page.
4. Preview locally, then commit and push (see below).

## Edit or add a page

- **Home / About-style text:** edit `_pages/index.md` (or other files in `_pages/`).
- **Category landing pages** (grid of posts): e.g. `_pages/life.md`, `_pages/society.md`. Front matter sets `taxonomy` to the category name and `permalink`.
- **New nav tab:**
  1. Add `_pages/your-page.md` with `layout: category`, `taxonomy: your-category`, `permalink: /your-category/`.
  2. Add an entry in `_data/navigation.yml`.
  3. Use that category name in new posts’ `categories:`.

## Update the repo / publish

GitHub Pages builds from `main`. Typical flow:

```bash
git status
git add _posts/ assets/images/ _pages/ _data/navigation.yml   # only what you changed
git commit -m "Add Budapest Danube cruise life post"
git push origin main
```

Avoid staging `_site/`, `.bundle/`, or local gem caches.

After push, wait a minute for Pages to rebuild, then check the live site.

## Common tweaks

- **Nav labels / order:** `_data/navigation.yml`
- **Site title, subtitle, author:** `_config.yml` (restart `jekyll serve` after changes)
- **Bio sidebar photo / links:** usually under `_config.yml` author settings and `assets/images/`
- **Teaser on category grids:** set `header.teaser` in the post front matter
