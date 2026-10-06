# music-catalog-masu (data)

Actual catalog data for the [`music-catalog` CLI](https://github.com/sandorkazi/music-catalog)
(`git@github.com:sandorkazi/music-catalog.git`). Git-tracked so every
worktree/agent/user sees the same thing after push/pull.

```text
state/catalog.json    # artists/tracks/aliases (source of truth)
state/review.json     # unknown queue + pending merges
state/snapshots/      # timestamped monitor diffs
```

Sync from the code repo:

```bash
bash ../music-catalog/scripts/sync-data.sh pull
# ... run catalog ...
bash ../music-catalog/scripts/sync-data.sh push
```

Secrets are never committed here (env / `*.local.json` only).
SQLite (if added later) is a derived cache, never the authority.
