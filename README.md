# music-catalog-masu (data)

Actual catalog data for the [`music-catalog` CLI](https://github.com/sandorkazi/music-catalog)
(`git@github.com:sandorkazi/music-catalog.git`). Git-tracked so every
worktree/agent/user sees the same thing after push/pull.

```text
state/catalog.json    # artists/tracks/aliases (source of truth)
state/review.json     # unknown queue + pending merges
state/snapshots/      # timestamped monitor diffs
docs/graph.json       # generated Pages browser data (from state/catalog.json)
docs/index.html       # generated Pages browser page (viewer, no artwork hosted)
code/                 # submodule: music-catalog generator pinned to the built docs/
```

Live visualisation: GitHub Pages serves one combined site from the
`gh-pages` branch — `/` is main's browser, `/develop/` is develop's
(`https://sandorkazi.github.io/music-catalog-masu/` and `.../develop/`).
`Settings → Pages → Deploy from branch → gh-pages / (root)`, rebuilt
automatically by `.github/workflows/pages.yml` on every push to
`main`/`develop` that touches `docs/`.
Regenerate after catalog changes (from the code checkout):

```bash
bash ../music-catalog/scripts/publish-viz.sh         # render + commit docs/
bash ../music-catalog/scripts/publish-viz.sh --check # exit 1 if docs/ went stale
```

Each export stamps `docs/graph.json → meta` (`catalog_sha256` +
`generated_at`); the page header shows it, so staleness is visible
and checkable without rebuilding.

Sync from the code repo:

```bash
bash ../music-catalog/scripts/sync-data.sh pull
# ... run catalog ...
bash ../music-catalog/scripts/sync-data.sh push
```

Secrets are never committed here (env / `*.local.json` only).
SQLite (if added later) is a derived cache, never the authority.
