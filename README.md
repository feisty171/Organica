# Organica International — frontend handoff

Static storefront prepared for backend integration.

## Repository structure

```text
.
├── index.html, house.html, shop.html, learn.html
├── product-juve.html, product-mask.html, product-prepe.html
├── assets/
│   ├── css/                 # Site styles
│   ├── js/                  # Frontend behaviour
│   ├── images/
│   │   ├── brand/           # Logo
│   │   ├── house/           # Brand history and laboratory imagery
│   │   ├── products/        # Collection and product galleries
│   │   ├── science/         # Optimized Science-card imagery
│   │   └── video/           # Video thumbnails
│   └── source-artwork/      # Original supplied artwork, not served directly
└── README.md
```

Keep new production images in the relevant `assets/images` category. Preserve editable or original campaign files in `assets/source-artwork` and generate web-optimized derivatives for the site.

## Pages

- `index.html` — landing page
- `house.html` — brand story and contact
- `shop.html` — collection overview
- `product-juve.html` — JUVE product page
- `product-mask.html` — Bright+ Mask product page
- `product-prepe.html` — ProBio Prepé product page
- `learn.html` — Science articles, videos, and product FAQs

The former Model page and all site navigation to it have been removed.

## Backend integration points

- Cart, checkout, authentication, account balances, referrals, and delivery dates
- Contact and newsletter form submission
- Live bottles-shipped counter (`[data-live-value]`)
- Final commercial pricing where the interface says “Price on request”

No fabricated review data or customer testimonials are included. Account values use neutral empty states until live data is supplied.

## Local preview

Run a static server in this directory, for example:

```sh
python3 -m http.server 8765
```

Then open `http://localhost:8765/index.html`.
