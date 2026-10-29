# Port plan: lawrencelaplue.com → GitHub Pages

Written 2026-10-28.

## Where things stand

- **Current host:** WordPress.com (paid plan, because it carries a custom domain).
- **Domain:** `lawrencelaplue.com`, with DNS served by WordPress.com (`ns1-3.wordpress.com`), so it is most likely registered through WordPress.com too.
- **Email on the domain:** the MX records point to **Zoho Mail**. If you have, or ever gave out, an `@lawrencelaplue.com` address, it stops working when the domain lapses. Check this before you drop the domain.
- **Content (6 URLs):**

  | Page | Current URL | Content |
  |---|---|---|
  | Home | `/` | Bio, family photo, contact info |
  | Teaching | `/teaching-2/` | Course list, 2 syllabus PDFs, external links |
  | Research | `/research/` | Papers, many PDFs, DOI links, 2 SharePoint links |
  | CV / About | `/curriculum-vitae/` | CV PDF, bio, photo |
  | Blog | `/blog/` | One post |
  | Rent vs Buy (2017) | `/2017/05/25/rent-vs-buy/` | Text, `rvb5.xlsx` download |

- **Features that go away on a static site:** comments, sidebar search, likes, share buttons, email subscriptions, and the WordPress.com bar. None of them seem essential to an academic site.

## Target

- **Repo:** `github.com/lawlap/lawlap.github.io` (public, which free GitHub Pages requires).
- **New URL:** `https://lawlap.github.io`. You can add a custom domain later at any time.
- **Format:** plain HTML + one CSS file, with no build step. There are six pages and they rarely change, so a generator (Jekyll, Hugo, Quarto) would add more upkeep than it saves. This can be revisited if the blog grows.
- **Layout:**
  ```
  index.html          Home
  teaching/index.html
  research/index.html
  cv/index.html
  blog/index.html
  blog/rent-vs-buy/index.html
  404.html
  files/              PDFs, xlsx, CV (original WordPress file names)
  img/                photos and header image
  css/style.css       matches the old "Big Brother" theme
  teaching-2/, curriculum-vitae/, 2017/05/25/rent-vs-buy/
                      forwarding pages at the old WordPress addresses
  ```

  The header, menu, sidebar and footer are copied into each page. To change the menu or contact box, edit all six pages plus `404.html`.

## Steps

### 1. Back everything up (do this first, while the site is still live)
- [x] WordPress.com dashboard → **Tools → Export → Export all**. This downloads a `.zip` with an XML file of all posts and pages.
- [x] Same screen → **Export media library**. This downloads every PDF and image.
- [x] Saved both to `OneDrive - New Mexico State University\website\`. They are a one-time backup, not working files.
- [ ] Copy any blog comments you want to keep. They are in the export XML, but they won't be displayed on the new site.

### 2. Build the new site (Claude can do most of this)
- [x] Put the exported media in `files/` and `img/`. Bring over only the files the pages actually link to.
- [x] Recreate the six pages as HTML. Keep the text as it is, and update anything stale (course list, papers, CV PDF).
- [x] Add a `404.html` page.
- [x] Preview locally and check every link.

### 3. Publish
- [ ] Push to `main`.
- [ ] GitHub repo → **Settings → Pages → Source: Deploy from a branch → `main` / root**.
- [ ] Confirm that `https://lawlap.github.io` loads and every PDF link works.

### 4. Repoint the world to the new URL
- [ ] Update the website link in: your CV PDF, NMSU faculty profile, Google Scholar, ORCID, RePEc/IDEAS, SSRN, LinkedIn, and your email signatures.
- [ ] Search your published papers and working papers for `lawrencelaplue.com`. Printed links can't be changed, which is part of the case for keeping the domain (see the decision below).

### 5. Wind down WordPress.com
- [ ] Turn off auto-renew for the plan, so it lapses at the end of the current term. Don't cancel early unless you get a refund.
- [ ] Optional: before it lapses, add a line to the old home page saying "This site has moved to lawlap.github.io".
- [ ] Decide what happens to the domain (below) **before** its renewal date.

## Decision: keep or drop the domain?

**Status (2026-10-28):** undecided. The current term runs about 10 more months (to roughly Aug 2027; check the exact date in WordPress.com → Upgrades → Domains). Decide at least a month before renewal, because a transfer to another registrar can take up to a week.

| | Drop it | Keep it (~$12–20/yr at a registrar such as Cloudflare or Porkbun) |
|---|---|---|
| Cost | $0 | Domain fee only; hosting stays free |
| Old links in papers/CVs | Break | Keep working |
| Zoho email on the domain | Dies | Keeps working (move the MX records to the new registrar) |
| Risk | Someone else can buy the name and put content under it | None |

If you keep it: transfer the domain out of WordPress.com to a cheap registrar, point it at GitHub Pages (four `A` records plus `www` CNAME → `lawlap.github.io`), copy over the Zoho MX/SPF/DKIM records, and add the domain under repo **Settings → Pages → Custom domain**.

If you drop it: let it expire after step 4 is done, and turn off Zoho on that domain first.

## Folder setup (decided)

- **Working copy:** `C:\dev\lawlap.github.io`, next to your other projects in `C:\dev`.
- **Not in OneDrive.** OneDrive sync and `.git` folders conflict: they cause locked files, duplicate "-PC" copies, and corrupted history. GitHub is the backup for this folder.
- **OneDrive is only for** the one-time WordPress export (step 1) and any large source files you don't want in the repo.
