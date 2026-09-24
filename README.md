# Organica International — frontend handoff

Static storefront prepared for backend integration. Live at [organicaintl.com](https://organicaintl.com), served from a Tencent Lighthouse VM behind Cloudflare.

## Repository structure

```text
.
├── index.html, house.html, shop.html, learn.html
├── product-juve.html, product-mask.html, product-prepe.html
├── product-elixir.html, product-repair.html
├── assets/
│   ├── css/                     # Site styles (style.css)
│   ├── js/                      # Frontend behaviour (app.js) — carousels, language
│   │                             switching, mobile nav, product galleries, etc.
│   ├── images/
│   │   ├── brand/                # Logo
│   │   ├── hero/                 # Homepage hero banners (desktop + mobile variants)
│   │   ├── landing/               # Homepage "explore" card imagery
│   │   ├── products/              # Collection and product galleries
│   │   ├── collection/            # Shop page imagery
│   │   ├── science/               # Science-card imagery
│   │   ├── video/                 # Video thumbnails
│   │   └── Our heritage image /   # House-page timeline photos (note the trailing
│   │                               space in this folder name — it's real, matches
│   │                               existing HTML references, don't "fix" it without
│   │                               updating every reference to it)
│   └── source-artwork/           # Original supplied artwork, not served directly
└── README.md
```

Keep new production images in the relevant `assets/images` category, sized close to their actual display dimensions and compressed before committing — several images were previously committed at 10-20MB+ each (full camera/export resolution with no compression), which was the single biggest factor in page load time. Prefer JPEG for opaque photos and reserve PNG for images that need transparency. Preserve editable or original campaign files in `assets/source-artwork` and generate web-optimized derivatives for the site.

## Pages

- `index.html` — landing page
- `house.html` — brand story, heritage timeline, and contact
- `shop.html` — collection overview
- `product-juve.html` — JUVE product page
- `product-mask.html` — Bright+ Mask product page
- `product-prepe.html` — ProBio Prepé product page
- `product-elixir.html` — Orchid Idebenone Elixir Glow product page
- `product-repair.html` — Repair+ Skin Rescue Concentrate product page
- `learn.html` — Science articles, videos, and product FAQs

This is a traditional multi-page site (not a single-page app) — each page above is a real, separate HTML document linked with normal `<a href>` tags, so navigating between them is a genuine page load by design. In-page interactions (language switcher, mobile drawer, carousels, product image galleries, accordions) are handled by `assets/js/app.js` without a reload.

## Multi-language support

The site supports English, 中文, ไทย, 한국어, and 日本語 via the globe icon in the header (`setLang()` in `app.js`, persisted to `localStorage`). The desktop nav automatically falls back to the mobile hamburger menu whenever the translated labels don't actually fit next to the logo (`fitNav()` in `app.js`), rather than relying on a single fixed viewport breakpoint tuned for English — this matters because translated labels vary significantly in length.

## Backend integration points

- Cart, checkout, authentication, account balances, referrals, and delivery dates
- Contact and newsletter form submission
- Live bottles-shipped counter (`[data-live-value]`)
- Final commercial pricing where the interface says “Price on request”

No fabricated review data or customer testimonials are included. Account values use neutral empty states until live data is supplied.

## Local preview

Run a static server in this directory, for example:

```sh
python3 -m http.server 8080
```

Then open `http://localhost:8080/index.html`.

## Production deployment

The site is deployed to a Tencent Lighthouse Ubuntu VM (`43.163.98.143`) running Nginx, with `organicaintl.com` and `www.organicaintl.com` pointed at it through Cloudflare (proxied — Cloudflare terminates SSL at the edge; the origin currently serves plain HTTP on port 80).

To ship a change:

```sh
git push origin main
ssh -i ~/.ssh/organica_lighthouse ubuntu@43.163.98.143 'bash ~/deploy.sh'
```

`deploy.sh` (on the server, in the `ubuntu` home directory) pulls the latest `main` from GitHub into `~/organica-repo`, syncs it into the Nginx web root at `/var/www/organicaintl`, and reloads Nginx. There's no CI/CD watching the repo — pushing to GitHub alone does not update the live site, the deploy step above has to be run explicitly each time.

When editing `assets/css/style.css` or `assets/js/app.js`, bump the `?v=NN` cache-busting query param on their `<link>`/`<script>` tags across all HTML pages, otherwise Cloudflare and visitors' browsers may keep serving a stale cached copy after deploy.
