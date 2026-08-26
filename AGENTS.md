# AGENTS.md

## Cursor Cloud specific instructions

This repository is a **purely static website** (a Traditional Chinese commemorative book, 陸軍官校四十四期裝甲兵畢業50週年紀念冊). There is no build system, package manager, backend, or test suite in the repo — just flat HTML pages at the repo root, one `style.css`, and PDF/image assets under `content/`.

### Running the site (development)

Serve the repo root with any static file server, then open `index.html`. Example:

```
python3 -m http.server 8000
```

Then browse `http://localhost:8000/`. `python3` is preinstalled, so no dependency install is needed. Do not just open the files via `file://` — some pages use `fetch()` and relative asset paths that work best over HTTP.

### Non-obvious notes

- **No lint / test / build steps exist.** There is nothing to install or compile; the "update script" is intentionally a no-op.
- **Guestbook + visit counter are backed by an external Google Apps Script** endpoint (hard-coded in `index.html` and `guestbook.html`). It is Google-hosted and cannot be run locally. When reachable, submitting the guestbook form actually writes a live message (verified working); the pages degrade gracefully (e.g. "無法取得") if the endpoint is blocked. Avoid submitting throwaway guestbook messages against the live backend unless intentionally testing it.
- **Google Fonts and Google Analytics (gtag.js)** are loaded from external CDNs; the site renders fine with fallback fonts if they are blocked.
- Production hosting is GitHub Pages at `https://44armor.github.io/50/`.
