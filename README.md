# CraftHub static catalogue

This repository hosts the server-free CraftHub catalogue.

- `mcaddons.json` — the full catalogue (same shape as `/api/v1/catalog`).
- `media/covers/` — one cover image per item.
- `media/gallery/` — screenshots referenced by the items.

The app loads it directly from:

```
https://raw.githubusercontent.com/maghribispace/work/refs/heads/main/mcaddons.json
```

## Updating the catalogue

1. Edit the catalogue in the CraftHub admin panel (or import items through the
   JSON API).
2. Export a fresh static bundle:

   ```bash
   cd server
   .venv/bin/python tools/export_static.py \
     --server http://127.0.0.1:8000 \
     --base-url https://raw.githubusercontent.com/maghribispace/work/refs/heads/main \
     --out ../github-bundle
   ```

3. Copy the contents of `github-bundle` here (`mcaddons.json` and `media/`),
   then commit and push to `main`.

## Notes

- No server is required at runtime. Covers, screenshots and packs are plain
  files served by GitHub.
- Install/like counters are read-only in this mode because there is no server
  to record taps.
- GitHub's raw CDN caches files for about five minutes, so a fresh push can
  take a few minutes to show up everywhere.
- Only publish media and packs you own or are allowed to redistribute.
