# shwelinyone-ui-assets

UI assets for **novabett-2dlive** (ရွှေလင်းယုန် / Shwe Linyone) — brand
logo, avatars, payment/method icons, footer labels, admin icons, etc.
Cloudflare Worker static assets, served from a dedicated domain, same
pattern as `imbet69-ui-assets`.

This is a **separate repo/Worker/domain from `imbet69-ui-assets`** — keeps
novabett-2dlive's asset traffic isolated so a bad file/deploy here can
never affect iMBET69, and vice versa.

## Folder structure

Deterministic paths, one folder per asset category (folders below are a
starting scaffold — add more as needed, following the same
`ui/{category}/{file}` shape):

```
ui/
├── brand/    logo + wordmark (ရွှေလင်းယုန် hare mark, header assets)
├── avatar/   {n}.webp        (profile avatar picker)
├── payment/  {method}.webp   (kpay, wave)
├── footer/   {label}.webp
├── admin/    *.webp          (AdminDashboard / AdminPaymentChannels icons)
└── misc/     anything not covered above
```

`.gif` files stay `.gif` (animated) — do not convert to webp. Everything
else → `.webp`.

## URL pattern (once the Cloudflare custom domain is attached)

```
https://{custom-domain}/ui/{category}/{file}
```

Domain to be attached by Yoh Homie via Cloudflare once this repo is
connected as a Worker/Pages project. novabett-2dlive should proxy this
same-origin via a Vercel rewrite once the domain is known (same pattern
already used on iMBET69: `/img/ui/(.*) → https://cdn.oraclemk.cloud/$1`),
so it never appears as a third-party domain in the browser.

## How to add/update files

1. New branch off `main` — **never commit straight to `main`**.
2. Add files under `ui/...` in the matching category folder (case-sensitive,
   no spaces in filenames).
3. `.gif` stays `.gif`. Everything else → `.webp`.
4. Open a PR. Do not merge it yourself — Yoh Homie or Claude reviews and
   merges. Cloudflare's GitHub integration only deploys on push to `main`,
   so a branch/PR never touches the live site.
5. Never force-push, never rewrite history, never touch `wrangler.toml`,
   folder structure, or any file outside `ui/` without asking first.
