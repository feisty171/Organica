# Organica — v7

## Two structural fixes this pass

**1. Layout unified, single source of truth.**
The nav dropdown's JUVE/Bright Mask links and the Collection's own
expand-on-click cards used to lead to two different, separately
maintained layouts — that's why they drifted apart. Fixed by removing
the duplication instead of just re-syncing it:
- product-juve.html and product-mask.html are now tiny redirect stubs
  (meta refresh) pointing to shop.html#juve / shop.html#mask, so old
  links and bookmarks still work.
- shop.html reads the URL hash on load AND listens for hash changes,
  so every nav dropdown link, every footer link, and every "Explore
  JUVE" button on the landing page all open the exact same in-page
  panel — there is now only one implementation of the JUVE and Bright
  Mask detail views, not two.

**2. New magazine-style product layout**, matching the reference:
PRODUCT eyebrow → big serif name → description paragraphs on the
left, photo + short blurb on the right, then a FEATURES grid (bold
ingredient name + one-line role, two columns) below, then How to Use,
then the size/quantity/Add to Cart bar at the very bottom. Both JUVE
(real content) and Bright Mask (placeholder) use the identical
structure.

## Copy changes
- "The Edit" → "The Collection" everywhere, including the huge italic
  stage title.
- Cringe tagline removed. New line: "The full formula, not the
  highlight reel."
- Ingredient content re-sourced from the OPP deck's actual ingredient
  names and the hyaluronic acid water-binding fact — but the deck's
  drug-adjacent claims (BoNTLIF, "instant facelift," "eliminate signs
  of ageing in 30 days," specific wrinkle-reduction timelines) were
  deliberately left out, consistent with the HSA/drug-registration
  concern flagged earlier in this project. Everything else from the
  deck is in.

## Known gaps
- Bright Mask: still no real photo, price, or ingredients.
- New magazine-layout body copy (descriptions, features, usage) is
  translated for JUVE. Bright Mask's placeholder text is English-only
  by nature of being placeholder.
