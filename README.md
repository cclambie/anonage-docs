# AnonAge Docs

Public developer documentation for the AnonAge age-verification API, built with
[Mintlify](https://mintlify.com). This is the "GitHub backend" for the docs site — Mintlify
renders these files and serves them at the custom docs domain.

## Structure

```
docs.json                 Mintlify config (nav, theme, brand)
introduction.mdx          What AnonAge is + the flow
quickstart.mdx            End-to-end integration in ~10 min
authentication.mdx        API keys + the two secrets
webhooks.mdx              Callback contract + signature-verification recipes
testing.mdx               Sandbox / going live
api-reference/openapi.json  OpenAPI 3.1 spec — the source of truth for the reference
logo/, favicon.svg        Brand assets (placeholders — replace with real ones)
```

## Run locally

```bash
npm i -g mint      # Mintlify CLI (older name: `mintlify`)
mint dev           # serves at http://localhost:3000, validates docs.json
```

`mint dev` validates the config and OpenAPI — run it before pushing.

## Publish

1. Push this repo to GitHub (e.g. `cclambie/anonage-docs`).
2. In the [Mintlify dashboard](https://dashboard.mintlify.com), connect the repo. It redeploys
   automatically on every push to the default branch.
3. **Custom domain:** in Mintlify → Settings → Custom Domain, set `docs.anonage.io`, then add the
   CNAME record it shows you in Cloudflare (the anonage.io zone). This replaces the old
   `docs.test.ageget.com` docs site.

## Keeping it accurate

`api-reference/openapi.json` is the source of truth for the API reference — update it whenever the
API changes (endpoints live in `ageget-app-web/apps/api`). The base URLs are
`https://api.anonage.io` (production, coming) and `https://dev1api.anonage.io` (development).

> Notes:
> - The brand assets in `logo/` and `favicon.svg` are simple placeholders — swap for real ones.
> - `docs.json` is Mintlify's current config format; older setups used `mint.json`.
