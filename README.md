# Point Club PWA (GitHub Pages)

This package wraps the current Point Club HTML app as an installable Progressive Web App. It includes a web app manifest, icons, and a service worker for offline loading after the first successful visit.

## Publish to GitHub Pages

1. Create a GitHub repository, for example `point-club`.
2. Upload **the contents of this folder** to the repository root. `index.html` must be at the root, beside `manifest.webmanifest` and `service-worker.js`.
3. In the repository, open **Settings → Pages** and choose the branch and `/ (root)` folder as the publishing source.
4. Wait for GitHub Pages to publish. The address for a project site will look like `https://YOUR-USERNAME.github.io/point-club/`.
5. Open that HTTPS address in Chrome or Edge, wait for the app to load once while online, then use the browser's **Install app** option. On mobile, use the browser's **Add to Home Screen / Install** option if available.

All manifest, icon, and service-worker paths are relative, so the package works under a GitHub Pages project path as well as a site root.

## Google Drive OAuth setting

The app uses Google Identity Services. In Google Cloud Console, add your exact GitHub Pages origin as an **Authorized JavaScript origin**. For a project site, the origin is only `https://YOUR-USERNAME.github.io` (no `/point-club/` path). Keep the existing OAuth client ID unless you intentionally create a new one. Drive authorization still requires an online connection and may require reconnecting when the access token expires.

## Important behavior

- Task, achievement, reward, and history data are stored in this browser's local storage; this package does not upload them anywhere except when you explicitly use the app's Google Drive backup features.
- The service worker caches the app shell so the app can open offline after its first successful online load. Google Drive features cannot work offline.
- Browser local storage is scoped to the new HTTPS site. Data from the old `file://` HTML version will not automatically transfer. Use the old app's backup/export function, then restore/import it in the hosted app.
- This static PWA cannot guarantee a Google Drive upload while the app is fully closed. Browser background scheduling is best-effort, not a reliable server-side timer.
- After changing app files, the service worker may briefly show a cached version while updating. The cache version is in `service-worker.js` (`CACHE_VERSION`); increment it for future releases.
