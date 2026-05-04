# tytus-app-catalog

Curated catalog of Featured apps for the [Tytus OS](https://github.com/traylinx/tytus-os) App Store. The shell fetches `featured.json` from this repo at boot and shows the entries in the App Store's "Featured" section with one-click Install.

## Why a separate repo

Adding a new featured app — or bumping a featured app's pinned tag — should NOT require an OS release. This repo is the source of truth; the App Store fetches it via jsDelivr each session, falling back to a hardcoded built-in catalog if the fetch fails.

## Schema

```jsonc
{
  "version": 1,
  "updatedAt": "ISO-8601 timestamp",
  "apps": [
    {
      "id": "<canonical app id>",
      "name": "<display name>",
      "description": "<one-line summary>",
      "icon": "<lucide icon name>",
      "category": "Productivity | DevTools | Media | Creative | ...",
      "manifestUrl": "<https URL to the app's tytus-app.json>"
    }
  ]
}
```

## Adding an app

1. Publish your app to its own public repo at `github.com/<owner>/tytus-app-<id>`.
2. Tag a `v0.X.Y` release with a built `dist/index.js` + `tytus-app.json`.
3. Open a PR here adding an entry to `apps[]`.
4. Merge → tag a new `v0.X.Y` of `tytus-app-catalog` → users see your app the next time the App Store refreshes.

## Versioning

`tytus-app-catalog` itself is tag-pinned. The Tytus OS shell fetches:

```
https://cdn.jsdelivr.net/gh/traylinx/tytus-app-catalog@v0.2.0/featured.json
```

Current Tytus OS builds reference `v0.2.0`. Bump the catalog tag whenever you ship a meaningful change; bump the constant `FEATURED_CATALOG_URL` in `app/src/apps/featured-apps-catalog.ts` (tytus-os) and the corresponding constant in `cli/src/main.rs` (tytus-cli) when a new tag should become the default.

## License

MIT — see `LICENSE`.
