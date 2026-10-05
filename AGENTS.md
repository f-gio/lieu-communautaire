# AGENTS.md

## What this is

French-language PWA for a community site ("Tiny Houses — Lieu communautaire").
No build system, package manager, tests, lint, or CI. The app is almost entirely
`index.html` (~6000 lines: CSS + HTML + several script blocks) plus PWA assets.

Git remote: `https://github.com/f-gio/lieu-communautaire`, branch `main`.
History is mostly GitHub web uploads ("Add files via upload"); `index.html` is the source of truth.

## Architecture

- `index.html` — the whole app (design-system CSS, section UI, Firebase client JS).
- `service-worker.js` — PWA shell cache.
- `manifest.webmanifest`, `apple-touch-icon.png`, `icons/` — install assets.
- Backend = Firebase Auth + Firestore (project `lieu-communautaire`), config embedded in
  `index.html`. No server code, no `firebase.json`, no Firestore rules in this repo —
  security rules and account approval live in the Firebase console.

### Inside `index.html`

1. `<style>` — Design System tokens in `:root`. In-file rule: new colors, spacing, radii,
   and shadows must use tokens. Historical aliases (`--ink`, `--forest`, `--sage`, …) remain
   and are still referenced by older rules — keep them until fully migrated.
2. HTML — nav `#nav button[data-page="…"]` toggles `<section id="…">` blocks
   (`dashboard`, `principles`, `resources`, `budget`, `tasks`, `calendar`, `community`,
   `polls`, `notes`, `history`).
3. Scripts — Firebase ESM imports from `https://www.gstatic.com/firebasejs/12.2.1/…`
   (page **must be served over HTTP(S)**, not `file://`), then several design-system IIFE
   blocks (toasts, modals, nav state, password UI, …).

Late CSS layers intentionally override earlier rules with `!important` (responsive fixes,
horizontal header). An override turns the original `.side` sidebar into a sticky top bar.
Do not reorder or "clean up" cascade without checking desktop + mobile.

### Firestore data model (hard-coded in JS)

- `users/{uid}` — profile, `role` (`member`/`admin`), `status`
  (`pending`/`approved`/`rejected`/`suspended`)
- `publicMembers/{uid}` — member directory
- `projects/maison-demain` — project doc + subcollections `calendar`, `resources`, `notes`,
  `polls`, `notifications`, `history`
- Nested: `taskComments/{taskId}/comments`, note reactions,
  `users/{uid}/notifications`, `users/{uid}/notificationReads`

Admin: `ADMIN_UID` is hardcoded in `index.html`; `isAdmin()` also honors `role==='admin'`.
Signup writes `status:'pending'`; live UI access is blocked until an admin approves the account.

### Legacy → collaborative data (easy to break)

The project doc still holds embedded arrays (`calendarEvents`, `resources`, `noteItems`,
`polls`) and `collaborativeMigrationVersion`. Loads go through `collaborativeOrLegacy(fresh, legacy)`:
Firestore collections win when non-empty; otherwise legacy arrays are shown.
Preserve this path when touching data loading.

## Deploy gotchas

- `service-worker.js` sets `CACHE_NAME='tiny-houses-app-v10-5-20260914'`.
  **Bump this string on every content deploy** (e.g. `tiny-houses-app-v10-5-YYYYMMDD`) or
  installed PWAs keep serving stale `index.html` from cache.
- Navigations are network-first with cache fallback; other same-origin GETs are cache-first.
  New shell assets must be added to `APP_SHELL` to be pre-cached.

## Working on the UI

- User-facing strings are **French only** (labels, toasts, errors). Match existing tone.
- Prefer the global feedback API (defined in a late script block):
  `window.showToast(message, type)`,
  `window.setActionLoading(button, loading, label)`,
  `window.confirmAction({ title, message, confirmLabel, danger })`.
- Log entity changes via `logHistory(...)`; some creations also call `publishNotification(...)`.
- Profile photos are compressed client-side to ≤5 KB (stored as base64 in Firestore).

## How to verify (no test suite)

1. Serve the repo root statically, e.g. `python -m http.server 8080`, open
   `http://localhost:8080/`. Firebase ESM imports fail on `file://`.
2. DevTools console: boot must clear `body.auth-pending`. The app stays blank until Firebase
   auth resolves — a boot error here is the usual failure mode.
3. Full auth-gated flows need a Firebase test account and admin approval in the Firebase console
   (outside this repo).
4. After UI or shell changes: bump `CACHE_NAME`; hard-refresh or unregister the SW when
   testing locally.

## Conventions that differ from defaults

- No npm/Node toolchain — do not introduce `package.json`, bundlers, or frameworks unless asked.
- Do not split `index.html` into modules/components without an explicit request; the workflow
  is edit-in-place + deploy.
- Firebase web config in the client is intentional; enforce access with Firestore rules, not
  by hiding code.
