# 🎬 kiz-ytdlp — Private yt-dlp Feed for KIZ Player

![yt-dlp](https://img.shields.io/badge/yt--dlp-2026.08.19-brightgreen)
![feed](https://img.shields.io/badge/feed-stable-blue)
![license](https://img.shields.io/badge/license-MIT-orange)

> The **only** source KIZ Player trusts for its download engine.
> No official servers, no PyPI — just this repo. 🔒

---

## ✨ What is this?

KIZ Player downloads music through **yt-dlp** running on-device.
Instead of shipping a frozen engine forever, the app checks this repo
for new builds and installs them **from inside the app** — safely:

- ✅ New binary is **test-run on the phone before activation**
- ✅ Broken files are **rejected before they can do harm**
- ✅ The working engine is **backed up & auto-restored** on any failure

So updating the downloader for every user = **upload 2 files here**. That's it. 🚀

---

## 📦 Repo layout

| File | What it is |
|---|---|
| `latest.txt` | One line — the current version, e.g. `2026.08.19` |
| `yt-dlp` | The standalone yt-dlp **zipapp binary** (exact bytes, no extension) |
| `CHANGELOG.md` | What changed per engine version |
| `README.md` | You are here 👋 |

The app reads exactly these two URLs:

```text
https://raw.githubusercontent.com/rkkizar777-design/kiz-ytdlp/HEAD/latest.txt
https://raw.githubusercontent.com/rkkizar777-design/kiz-ytdlp/HEAD/yt-dlp
```

> ⚠️ Keep both filenames **exactly** as shown — the app hardcodes them.

---

## 🔌 How the app consumes this feed

1. **Settings → engine card** asks `latest.txt` for the newest version.
2. If it's newer than the installed one → *"Update available"* 🎉
3. Tap **Update** → the app downloads `yt-dlp` and runs the gauntlet:
   - ❌ Reject if under ~1 MB or structurally invalid
   - ❌ Reject if it won't report `--version` on the phone's Python
   - 💾 Back up the working engine, swap, re-verify
   - ↩️ Auto-restore the backup if the new one misbehaves

A bad upload **can never break downloads**. 🛡️

---

## 🚀 Publish an engine update

1. Grab a fresh `yt-dlp` zipapp from the
   [official releases](https://github.com/yt-dlp/yt-dlp/releases).
2. Upload/replace the `yt-dlp` file in this repo (web UI drag & drop works).
3. Edit `latest.txt` → new version on **one line** (e.g. `2026.09.01`).
4. Add a `CHANGELOG.md` entry (copy the format below).
5. Update the badge at the top of this README to the new version. 🏷️
6. Open KIZ Player → **Settings → engine → Update**. Done! ✅

### Format contract (don't break these)

- `latest.txt` must match `YYYY.M.DD` → regex `\d{4}\.\d{1,2}\.\d{1,2}`
- `yt-dlp` must be a runnable **zipapp** (`python yt-dlp --version` works)
- Both files live in the **repo root** on the default branch

---

## 🧑‍💻 For developers — fork it & make it yours

Want this feed for your own app? Fork it! 🍴

1. **Fork** this repo to your account.
2. In your app, point the two URLs at your fork:
   ```text
   https://raw.githubusercontent.com/YOU/kiz-ytdlp/HEAD/latest.txt
   https://raw.githubusercontent.com/YOU/kiz-ytdlp/HEAD/yt-dlp
   ```
   (In KIZ Player these live in
   `app/src/main/java/com/kiz/player/youtube/YouTubeRepository.kt`
   as `kizYtdlpVersionUrl` / `kizYtdlpBinaryUrl`.)
3. Implement the same safety order client-side:
   `size check → structure check → on-device --version probe →
   backup → swap → re-verify → rollback on failure`.
4. Publish updates exactly like [above](#-publish-an-engine-update). 🎉

PRs improving docs, tooling or the safety checklist are welcome! 💡

---

## 🤝 Contributing

- 🐛 Found a bad engine build? Open an issue with the version + device.
- 📝 Docs fixes: PR directly against `main`.
- ⛔ Don't commit anything except the files in [Repo layout](#-repo-layout)
  plus docs — the feed must stay tiny and predictable.

---

## 📄 License

- Repo tooling & docs: **MIT** — see [LICENSE](LICENSE). Copy, fork, build. 💪
- The `yt-dlp` binary is the work of the
  [yt-dlp project](https://github.com/yt-dlp/yt-dlp) (public domain,
  [The Unlicense](https://github.com/yt-dlp/yt-dlp/blob/master/LICENSE)).
  All credit for the downloader goes to them. 🙏

---

<p align="center">Made for <b>KIZ Player</b> 🎵 — updates without app releases.</p>
