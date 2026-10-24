# sqlnikon.com

Doug Purnell's blog: SQL Server, photography, and the backyard BBQ. Built with
[Hugo](https://gohugo.io) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod)
theme, and served by GitHub Pages from `main`.

**This repository is public.** Never commit the WordPress export, which holds
commenters' email and IP addresses. It lives in the private `dcpurnell/SQLNikon`
repository along with the script that converted the old posts.

## Writing a post

```sh
hugo new posts/2026-11-02-my-post-title.md   # creates a draft from archetypes/posts.md
hugo server -D                               # preview at http://localhost:1313, drafts included
```

Edit the new file in `content/posts/`, set `draft: false`, commit and push.
GitHub Actions builds and publishes the site within a couple of minutes.

The URL comes from the date and `slug`: `/2026/11/02/my-post-title/`. Put images
for a post in `static/images/<year>/` and link them as `/images/<year>/file.jpg`.

Code blocks take a language for highlighting: ` ```sql `, ` ```powershell `.

## Adding a photo walk

```sh
hugo new photography/2026-11-15-greensboro-arboretum.md
```

Fill in the location and the SmugMug gallery link, then for each photo:

1. Resize to about 1600px on the long side, a few hundred KB.
2. Strip its metadata, including GPS location: `exiftool -all= photo.jpg`.
3. Put it in `static/photography/<file name without .md>/` and list it in the
   post's `<div class="gallery">`.

Full-size originals stay on [SmugMug](https://sqlnikon.smugmug.com).

## What's where

| Path | What it is |
|---|---|
| `hugo.toml` | Site settings: title, menus, URL patterns, theme, Giscus comments |
| `content/posts/` | Blog posts, one Markdown file each. The 47 from 2011–2019 were converted from WordPress. |
| `content/photography/` | Photo walks. `_index.md` is the intro at the top of the page. |
| `content/about.md` | The About page |
| `static/wp-content/uploads/` | Images from the WordPress site, at their old paths so old links still work |
| `layouts/_partials/comments.html` | Archived WordPress comments plus Giscus for new ones |
| `assets/css/extended/sqlnikon.css` | Small style additions: galleries, floated images, comments |
| `.github/workflows/deploy.yml` | Builds with Hugo and publishes to GitHub Pages |
| `PLAN.md` | The WordPress migration plan and checklist |

## Old WordPress URLs

Posts keep their `/YYYY/MM/DD/slug/` addresses, categories stay at
`/category/<slug>/`, tags at `/tag/<slug>/`, the RSS feed is at both `/feed/`
and `/index.xml`, and `/author/admin/` redirects to About. All 138 URLs in the
old WordPress sitemap were checked against the build.

## Comments

Old comments are shown as "Archived comments" from each post's front matter.
New comments use [Giscus](https://giscus.app) and are stored as GitHub
Discussions in this repository, so commenters need a GitHub account. Moderate
them from the repository's Discussions tab.

## Theme updates

```sh
hugo mod get -u github.com/adityatelange/hugo-PaperMod
```

Preview locally before pushing.

## Hosting

| What | Where |
|---|---|
| Domain registration | Hover (renews 2027-01-26, auto-renew on) |
| DNS | Cloudflare |
| Website | GitHub Pages, built by `.github/workflows/deploy.yml` |
