# 75 Day Better

Static site for the 75 Day Better program. No build step — plain HTML, CSS and JS.
Vercel serves this repo root as-is; every push to `main` deploys.

## Layout

| Path | What it is |
| --- | --- |
| `index.html` | Sales page. Hero console, the six rules, reset demo, start-date planner, offer, FAQ. |
| `app/index.html` | The tracker people install on their phone. Date-aware, keeps the day count, enforces the reset. |
| `manifest.webmanifest` | PWA manifest — name, colors, icons, opens at `/app/`. |
| `sw.js` | Service worker. Network-first for pages, cache-first for assets, works offline. |
| `icons/` | App icons (192, 512, maskable 512, apple-touch 180, favicon 32). |

## Changing the checkout link

Near the bottom of `index.html`:

```js
var CHECKOUT_URL = "https://buy.stripe.com/REPLACE_WITH_YOUR_LINK";
```

Paste the Stripe payment link there. The buy button stays inert until you do — it
just scrolls to the offer section, so nothing 404s in the meantime.

## Changing the six rules

They live in two places and must match:

1. `index.html` — the `ITEMS` array (hero console) and the `.rule-row` blocks (rules table).
2. `app/index.html` — the `ITEMS` array.

## Colors

Defined once as CSS variables at the top of each file:
forest `#2F4438`, pale `#EAEFEA`, white `#FFFFFF`, grey `#DEDEDE`, mint `#A9DC9E`.
Dark mode redefines the same variables — don't hard-code a color anywhere else.

## Progress data

The tracker stores each person's board in their own browser (`localStorage`, key `d75_v1`).
No accounts, no server. Clearing site data resets their board.
