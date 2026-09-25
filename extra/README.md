# extra/ — raw playlist inputs (not state)

`state/` is the source of truth. This dir holds raw, unmodified playlist
dumps for re-import / auditing:

- `youtube-music-placeholder-PLM_wsshzeeqIjkv6oNNHWRAjizhz5pZoc.json` —
  yt-dlp flat dump (`yt-dlp --flat-playlist -J "<playlist-url>"`) of the
  masu "music-placeholder" YouTube playlist (103 entries, 2026-09-25).

Refresh:

```bash
yt-dlp --flat-playlist -J \
  "https://www.youtube.com/playlist?list=PLM_wsshzeeqIjkv6oNNHWRAjizhz5pZoc" \
  > extra/youtube-music-placeholder-PLM_wsshzeeqIjkv6oNNHWRAjizhz5pZoc.json
```

Cross-reference against the Spotify-built registry (read-only):

```bash
PYTHONPATH=src python3 -m music_catalog.cli xref \
  ../music-catalog-masu/extra/youtube-music-placeholder-PLM_wsshzeeqIjkv6oNNHWRAjizhz5pZoc.json --compact
# write path (adds new artists, queues unknowns, proposes merges — explicit only):
# PYTHONPATH=src python3 -m music_catalog.cli xref <file> --apply
```
