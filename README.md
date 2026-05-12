# tytus-app-catalog

Curated catalog of Featured apps for the [Tytus OS](https://github.com/traylinx/tytus-os) App Store. The shell fetches `featured.json` from this repo at boot and shows the entries in the App Store's "Featured" section with one-click Install.

## Why a separate repo

Adding a new featured app, or bumping a featured app's pinned tag, should NOT require an OS release. This repo is the source of truth; the App Store fetches it via jsDelivr each session, falling back to a hardcoded built-in catalog if the fetch fails.


## Current featured production apps

| App | Current pinned manifest | Notes |
|---|---|---|
| Atomek | `traylinx/tytus-app-atomek@v0.4.23/tytus-app.json` | Branded Tytus Resource Fabric cockpit, Monaco editor, intelligent chat, persistent workspace state, artifacts, AIL routing, embedded docs/skills, mission folders, OpenClaw/Hermes pods, local agents, shared folders, app skills, and approval-gated outputs. |

Keep app manifest URLs pinned to immutable app tags. The catalog pointer can move; app bundles should not.

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
2. Tag a release with a built `dist/index.js` + `tytus-app.json` (Forge currently uses `0.1.0`; older apps may use `v0.X.Y`).
3. Open a PR here adding an entry to `apps[]`.
4. Merge → tag a new `v0.X.Y` of `tytus-app-catalog` → users see your app the next time the App Store refreshes.

## Versioning

`tytus-app-catalog` itself is tag-pinned. The Tytus OS shell fetches:

```
https://cdn.jsdelivr.net/gh/traylinx/tytus-app-catalog@v0.2.0/featured.json
```

Current Tytus OS builds fetch the catalog from the mutable `main` branch so featured-app additions and Forge version bumps do not require an OS rebuild. Keep app manifest URLs pinned to immutable app tags; only this catalog pointer is mutable. For historical releases, tags such as `v0.7.0` remain available.

## License

MIT — see `LICENSE`.
