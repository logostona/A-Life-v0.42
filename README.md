# A Life — GitHub Pages deployment

This folder is a ready-to-host static build of the game. No build step needed —
GitHub just needs to serve these files as-is.

## Steps

1. **Create a new repository** on GitHub (public repos get free Pages hosting;
   private works too on paid plans). Any name is fine, e.g. `a-life`.
2. **Upload every file in this folder**, keeping the `icons/` subfolder intact:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `storage-polyfill.js`
   - `life-sim.bundle.js`
   - `icons/` (5 files)

   Easiest way: on the repo's GitHub page, click **Add file → Upload files**,
   drag in the whole folder, and commit.
3. **Turn on Pages**: repo → **Settings → Pages** → under "Build and deployment",
   set **Source: Deploy from a branch**, branch **main**, folder **/ (root)** →
   **Save**.
4. GitHub will give you a URL after a minute or two, in the form:
   `https://<your-username>.github.io/<repo-name>/`
5. Open that link on your phone → your browser's share/menu button →
   **"Add to Home Screen"** (iOS Safari) or **"Install app"** (Android Chrome).
   It'll behave like a native app icon, launching full-screen with no browser
   chrome.

## Notes on what's inside

- **`life-sim.bundle.js`** — the whole game (React + your `life-sim.jsx`)
  bundled into one self-contained file. Nothing is fetched from a CDN, so it
  works fully offline once installed.
- **`storage-polyfill.js`** — the game's save system was written to call
  `window.storage`, an API that only exists inside Claude's own artifact
  runtime. A plain browser (and therefore GitHub Pages) doesn't have it, so
  this file provides the same API backed by the browser's `localStorage`,
  meaning saves now genuinely persist between visits/sessions on your device.
- **`sw.js`** — a service worker that caches the app shell so it loads
  instantly and works with no signal/wifi after the first visit.
- Saves live in your browser's local storage, per-device — they won't sync
  between your phone and a laptop, and clearing site data / browser storage
  will wipe them, same as any local-only save.

## Updating later

If you get a new `life-sim.jsx`, ask for the bundle to be rebuilt and just
replace `life-sim.bundle.js` in the repo (upload the new file over the old
one, same name). Everything else stays the same.
