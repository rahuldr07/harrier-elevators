# Harrier Elevators

Marketing website for **Harrier Elevators** — lift installation, repair, service and
AMC, with branches in Bangalore, Telangana, Andhra Pradesh and Chennai.

Live at <https://harrier-elevators.com>

## What this is

A single-page static site. No build step, no backend, no package manager — the
contents of `dist/` are the website exactly as served.

```
dist/
├── index.html          the page
├── 404.html            not-found page
├── robots.txt
├── sitemap.xml
├── site.webmanifest
├── _headers            Cloudflare Pages caching + security headers
└── assets/
    ├── css/            bootstrap, fontawesome, owl carousel, magnific popup, style.css
    ├── fonts/          FontAwesome (woff2) + self-hosted Inter & Roboto
    ├── img/            photography, icons, favicon
    └── js/             jquery, bootstrap, owl carousel, wow, counter-up, main.js
```

## Local preview

No dependencies needed:

```sh
cd dist
python3 -m http.server 8899
```

Then open <http://localhost:8899>.

## Deployment

Deployed to **Cloudflare Pages** with the build output directory set to `dist`.
There is no build command — Pages serves the directory as-is.

`dist/_headers` controls caching (long-lived for `assets/`, always-revalidate for
the HTML) and sets `X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy`
and `Permissions-Policy`.

## Editing notes

- **Contact details** appear in the page body *and* in the JSON-LD `LocalBusiness`
  block in `<head>`. Change both, or search results will disagree with the page.
- **Fonts** are self-hosted. Inter and Roboto are single variable-weight `woff2`
  files, declared inline in `<head>` so the browser starts fetching them on the
  first parse. There is no external font request.
- **Images** are lazy-loaded below the fold and carry intrinsic `width`/`height`
  to avoid layout shift. Product and gallery tiles rely on `object-fit: cover`.
- **The page `<h1>`** lives outside the hero carousel on purpose — Owl Carousel
  clones slides for its infinite loop and would otherwise duplicate the heading.
- **Section anchors** (`#about`, `#products`, `#gallery`, `#contact`, plus one per
  lift type) are what the navigation links to.

## Origin

Recovered from a mirror of the previous host, then repaired and modernised:
broken assets restored, third-party analytics removed, navigation wired up,
accessibility and structured data added, and page weight cut from 13 MB to 6.2 MB.
