# kiz-ytdlp — KIZ Player's private yt-dlp feed

The app checks **only this repo** for download-engine updates. Nothing
else (no official yt-dlp, no PyPI) can ever change the engine.

## Files (repo root)

| File | Contents |
|---|---|
| `latest.txt` | One line: the version, e.g. `2026.08.19` |
| `yt-dlp` | The standalone yt-dlp zipapp binary (exact bytes, no extension) |

## Create the repo (5 minutes, on github.com)

1. New repository named **`kiz-ytdlp`** under `rkkizar777-design`
   (public, no README/license needed).
2. **Add file → Upload files**: drop in `yt-dlp` and `latest.txt`
   from this folder, then **Commit changes**.
3. Done. The app reads:
   - `https://raw.githubusercontent.com/rkkizar777-design/kiz-ytdlp/HEAD/latest.txt`
   - `https://raw.githubusercontent.com/rkkizar777-design/kiz-ytdlp/HEAD/yt-dlp`

## Publish an engine update later

1. Get a fresh `yt-dlp` zipapp (e.g. from
   `https://github.com/yt-dlp/yt-dlp/releases`).
2. In this repo: upload/replace the `yt-dlp` file, and edit
   `latest.txt` to the new version (one line, e.g. `2026.09.01`).
3. In the app: **Settings → engine → Update**.
   The app downloads the file, **test-runs it on the phone before
   activating**, keeps a backup of the working engine, and rolls back
   automatically if anything fails. A bad file can never break downloads.

## Safety rules the app enforces

- Version check and binary download use **only this repo**.
- Files under ~1 MB or failing a structural check are rejected.
- The candidate must report its `--version` on-device before the swap.
- The previous engine is restored if the new one fails after install.
