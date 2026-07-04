# Atarah Quiz — Live Scoreboard

A room-based scoreboard for the Atarah quiz event. One person hosts a room,
everyone else joins with the room code, and scores/team names/round names
sync across everyone in the room.

## Files

| File         | Purpose                                                          |
|--------------|-------------------------------------------------------------------|
| `main.html`  | The page markup and all app logic (JS)                           |
| `main.css`   | All styling (colors, fonts, layout, the crest background)         |
| `img.jpg`    | The Atarah crest artwork used as the full-page background        |
| `README.md`  | This file                                                         |

Keep all four files in the same folder — `main.html` links to `main.css`
and `main.css` links to `img.jpg` by relative path, so don't rename or
separate them.

## Opening it locally

Just double-click `main.html`, or right-click → **Open with** → your browser.
No build step, no install.

## ⚠️ Important: the "live sync" feature needs a real backend

The Host/Join room feature in this file was originally built using a
storage API that **only exists inside Claude.ai's artifact viewer** — it
is not a real database, and it does not work when `main.html` is opened
as a plain file (double-clicked, downloaded, or hosted on a normal web
server like GitHub Pages, Netlify, etc.). If you open these files outside
Claude.ai, hosting a room and joining it from another device **will not
sync** — each device will just see its own local copy, and joining a
room from another device will fail exactly like "no room found."

To get real cross-device sync outside Claude.ai, you have two options:

1. **Keep using it inside Claude.ai** — open the artifact from the same
   conversation on each device (not a downloaded file) and syncing works
   as designed.
2. **Wire up a real backend** — swap the `window.storage` calls in
   `main.html` for a small real-time database. The easiest free options:
   - **Firebase Realtime Database / Firestore** (Google, generous free tier)
   - **Supabase Realtime** (Postgres-backed, generous free tier)
   - A simple **WebSocket server** if you're comfortable running your own

   In `main.html`, every call to `window.storage.get(...)` and
   `window.storage.set(...)` would be replaced with the equivalent read/write
   calls for whichever backend you choose. The rest of the app (rendering,
   room codes, add/remove teams and rounds) doesn't need to change.

If you'd like, I can build you a version wired to Firebase or Supabase so
it works as a normal hosted website with real cross-device sync — just
share which one you'd prefer (Firebase is usually the faster path to set
up).

## Hosting it as a static site (without live sync)

If you just want a single-device or same-browser scoreboard (no
cross-device sync), any static host works as-is:

- **GitHub Pages**: push these 4 files to a repo, enable Pages in repo
  settings.
- **Netlify / Vercel**: drag-and-drop the folder onto their dashboard.

Either way, each browser/device will keep its own independent scoreboard
data since there's no shared backend behind it.
