# sqlnikon.com: WordPress to GitHub Pages

The WordPress hosting for sqlnikon.com expires on **December 8, 2026**. This plan
moves the blog to a Hugo site served by GitHub Pages before that date, using the
same two-repository layout as F3 Greensboro.

## Current state (checked 2026-10-24)

| Item | Detail |
|---|---|
| Blog posts | 47, June 2011 – March 2019 |
| Pages | About, Photography (empty, unchanged since 2019-01-04) |
| Media | 88 uploads under `wp-content/uploads/` |
| Categories | SQL Server (30), Professional Development (10), Elon (6), Apple (2), Uncategorized (0) |
| Tags | 86 |
| Comments | 11 |
| Post URLs | `/YYYY/MM/DD/slug/`, e.g. `/2019/03/25/consolidating-life/` |
| Domain | Hover, expires 2027-01-26, auto-renew on |
| DNS | Cloudflare (`val` / `jasper`.ns.cloudflare.com) |
| Email | None used. Leftover HostGator MX and SPF records to be removed. |
| SmugMug | https://sqlnikon.smugmug.com |

`dcpurnell/SQLNikon` already exists as a private repo holding a static HTML copy
of the site from August 2025, with a workflow deploying to Azure Static Web Apps
(`ashy-hill-0e57cc20f`). That copy is being thrown away and the repo reused.

## Repositories

| Repo | Visibility | Holds |
|---|---|---|
| `dcpurnell/sqlnikon.com` | **Public** | The Hugo site. GitHub Pages builds and serves it at sqlnikon.com. |
| `dcpurnell/SQLNikon` | Private | The WordPress export, the uploads backup, and the conversion script. |

**The public repo must never contain the WordPress export.** The export holds
commenters' email and IP addresses. Only post content, images, and the names and
text of the 11 comments go public.

Local folders: `~/Developer/sqlnikon.com` (public) and `~/Developer/SQLNikon`
(private).

## Generator: Hugo

- Single binary (`brew install hugo`). No Ruby or Node to maintain. Jekyll would
  need a newer Ruby than macOS ships (2.6).
- Builds and deploys from a GitHub Actions workflow on every push to `main`.
- Posts are Markdown files in `content/posts/`. Writing a post means adding a
  file and pushing.

## Theme options

Themes install as a Hugo module, so updating one is a single command and the
theme's files never mix with the site's.

| Theme | Look | Good at | Trade-offs |
|---|---|---|---|
| **PaperMod** | Clean single column, light/dark toggle | Fast, readable code blocks, built-in search, archive page, reading time, very widely used and maintained | Plain. Not image-forward, so Photography looks like a text list unless customised. |
| **Stack** | Cards with a left sidebar, feature image per post | Image-forward. Photography and posts with header photos look good. Built-in search, archives, Giscus support. | Busier. Needs a feature image per post to look its best, and most of the 47 posts don't have one. |
| **Blowfish** | Modern, Tailwind-based, many layouts | The most options: hero layouts, galleries, card lists per section | Large and configuration-heavy. More to learn than a blog this size needs. |
| **Congo** | Blowfish's simpler predecessor, Tailwind-based | Tidy, good typography, several colour schemes, dark mode | Fewer layout choices than Blowfish. |
| **Bear Cub / Hugo Bear Blog** | Minimal, almost no styling | Tiny and fast, nothing to break | No galleries, no search, very bare for Photography. |

**Chosen: PaperMod** (decided 2026-10-24). Most of this content is technical SQL
Server writing, and PaperMod's readability, code highlighting and search suit it.
If Photography grows into a main focus, Stack is the alternative to try.

Customisations on top of PaperMod, all in this repo:

- **Home page** (`layouts/home.html`): the bald eagle banner from the old site
  (`assets/images/eagle.jpg`, set in `params.hero`), then posts with a sidebar.
- **Sidebar** (`layouts/_partials/sidebar.html`) on the home page and every post
  (`layouts/posts/single.html`): About with the SQL Nikon logo, Recent Posts,
  Archives by year and month, Categories. On a post, its own year starts open.
  About and Photography stay single-column.
- **Favicon**: the SQL Nikon logo.
- Styles in `assets/css/extended/sqlnikon.css`.

## Site structure

```
sqlnikon.com/
  hugo.toml                 site config, permalinks, menus, Giscus settings
  content/
    posts/                  the 47 posts, one Markdown file each
    about.md
    photography/
      _index.md             intro + link to sqlnikon.smugmug.com
      <walk>.md             one file per future photo walk
  static/
    wp-content/uploads/     the 88 images, at their original paths
  layouts/                  home page, sidebar, post layout, archived comments
  .github/workflows/        Hugo build + Pages deploy
  .github/dependabot.yml    monthly pull requests to update the pinned Actions
  README.md                 how to write a post or add a photo walk
```

## Keeping old URLs working

| Old WordPress URL | New Hugo setting |
|---|---|
| `/2019/03/25/consolidating-life/` | `permalinks.posts = "/:year/:month/:day/:slug/"` |
| `/about/`, `/photography/` | Same paths |
| `/category/sql-server/` | `permalinks.categories = "/category/:slug/"` |
| `/tag/<tag>/` | `permalinks.tags = "/tag/:slug/"` |
| `/wp-content/uploads/...` images | Copied to the same paths under `static/` |
| `/feed/` (RSS) | RSS output also published at `/feed/index.xml` |
| `/page/2/` | Hugo's default paging path already matches |
| `/author/...` | Redirect to `/about/` |

After building, crawl every URL in the old sitemap against the preview and fix
any that return 404.

## Comments

- **The 11 existing comments** are converted to fixed text shown under their posts
  as "Archived comments": name, date and text only. No email, IP or website.
- **New comments** go through Giscus, which stores them as GitHub Discussions in the
  public repo. Setup (done): Discussions enabled, giscus app installed, threads
  in the Announcements category, mapped to each post by URL path.
  Commenters need a GitHub account. That suits a SQL audience.

## Photography

`/photography/` becomes a section, not a single page:

- `_index.md`: a short intro and a link to https://sqlnikon.smugmug.com.
- Each photo walk is its own Markdown file: date, location, 3–6 resized photos, and
  a link to the full SmugMug gallery. It appears on the Photography page
  automatically, newest first.
- Photos committed here are resized (~1600px long side, a few hundred KB) and have
  their metadata stripped (`exiftool -all=`). Full-size originals stay on
  SmugMug.
- Photography appears in the top menu next to About.

## Steps

### 1. Prepare
- [x] In WordPress admin, run **Tools → Export → All content** and save the `.xml`
- [x] Back up `wp-content/uploads/`: 118 files (88 originals plus resized copies)
      pulled from the live site into the private repo
- [x] Delete the Azure Static Web App `ashy-hill-0e57cc20f` (resource group deleted
      by Doug, 2026-10-24)
- [x] Wipe `dcpurnell/SQLNikon`: deleted and recreated private with one fresh commit
      (2026-10-24). No old branches or pull requests remain.
- [x] `brew install hugo` (0.168), plus `exiftool`

### 2. Private repo: archive and convert
- [x] Commit the WordPress export and uploads backup to `SQLNikon`
- [x] Write `scripts/convert.py`: WordPress XML → Hugo Markdown with front matter
      (title, date, slug, categories, tags, aliases), HTML → Markdown,
      SQL code blocks preserved, image links rewritten, comments extracted
      without email/IP
- [x] Spot-check posts with code samples, images and embeds

### 3. Public repo: build the site
- [x] Create public `dcpurnell/sqlnikon.com` and scaffold Hugo + PaperMod
- [x] Add the converted posts, About, images and the Photography section
- [x] Set permalinks, menus, RSS path and the author redirect
- [x] Add the archived-comments partial and Giscus
- [x] Add the GitHub Actions deploy workflow and turn on Pages (source: Actions)
- [x] Write `README.md`: how to write a post, add a photo walk, and change the theme

### 4. Preview and verify
- [x] Review at `https://dcpurnell.github.io/sqlnikon.com/` ("site looks great", 2026-10-24)
- [x] Crawl the old sitemap URLs (local build: 138/138): every post, tag, category and image resolves
- [x] Crawl every internal link on the preview (82/82)
- [x] Eagle banner and sidebar (home page and posts); checked at desktop and phone widths
- [ ] Skim code blocks, dark mode and phone layout on a real phone
- [ ] Post a test Giscus comment, then delete it from the repo's Discussions tab
- [x] Security audit (2026-10-24), see below

### Security audit (2026-10-24)

Clean: the WordPress export and commenters' emails/IPs are only in the private repo;
no secrets in the public repo's history; no GPS or camera data in public images;
archived comments contain no HTML; secret scanning and push protection are on;
Pages deploys only from `main`.

Fixed:
- [x] Pages publish rights (`pages: write`, `id-token: write`) moved to the deploy job.
      The build job is read-only.
- [x] Actions pinned to commit SHAs. Dependabot keeps them current; its first five
      pull requests were merged and deployed successfully (checkout v7, setup-go v7,
      configure-pages v6, upload-pages-artifact v5, deploy-pages v5).
- [x] An `http://` image changed to `https://`; the converter now upgrades WordPress.com links.
- [x] Private repo: removed a committed `__pycache__` file and ignored it.

Accepted: no branch protection on `main` (single author); the converter uses
Python's standard XML parser on Doug's own export.

### Preview vs live links

The preview lives under `/sqlnikon.com/`, so the deploy workflow's "Prefix post links
for the preview path" step adds that prefix to root-relative links in posts. Once the
custom domain is set, the base path is `/` and the step does nothing. Don't
re-enable `canonifyURLs`: it breaks the menu and paging links on the preview.

### 5. Cut over (target: mid-November, well before Dec 8)
- [ ] Verify sqlnikon.com for the `dcpurnell` account in GitHub Pages settings
      (Cloudflare TXT record `_github-pages-challenge-dcpurnell`)
- [ ] Cloudflare DNS:
  - [ ] Apex `A` records → 185.199.108.153, .109.153, .110.153, .111.153
  - [ ] Apex `AAAA` records → 2606:50c0:8000::153, 8001::153, 8002::153, 8003::153
  - [ ] `www` `CNAME` → `dcpurnell.github.io`
  - [ ] All set to **DNS only** (grey cloud) until GitHub issues the certificate
  - [ ] Delete the HostGator `MX` record and the `websitewelcome.com` SPF record.
        Add `v=spf1 -all` so nobody can send mail as sqlnikon.com.
- [ ] Set the custom domain in Pages settings and tick **Enforce HTTPS**
- [ ] Re-test the 138 old URLs on the live domain, and check the preview link-prefix
      step was skipped in the deploy log
- [ ] Submit `https://sqlnikon.com/sitemap.xml` to Google Search Console

### 6. Wind down
- [ ] Keep the WordPress site untouched until Dec 8 as a fallback
- [ ] Let the HostGator hosting expire. Do not renew.
- [ ] Domain renewal stays with Hover (next: 2027-01-26)

## Open decisions

None. Theme decided (PaperMod). Feature images are optional with PaperMod.

## Later, optional

- Restore the Dropbox downloads (marked "no longer available") into `static/files/`
  if the originals turn up.
- PaperMod links a `safari-pinned-tab.svg` that doesn't exist. Harmless.

## Next session

Pick up at step 4's two open items, then step 5. Say "start the cutover" to go
through the DNS changes one at a time.
