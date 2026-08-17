# Organica International — frontend handoff

Static storefront prepared for backend integration.

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
