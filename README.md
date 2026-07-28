# Work Flow Assist

A self-contained progress-tracking web app: editable task lists, completion
progress bars, per-task duration, and pop-up Gantt charts — with a Times New
Roman + gold/black theme. Works offline and installs to your phone/laptop.

## Files
- `index.html` — the whole app (HTML, CSS, and JavaScript in one file)
- `manifest.webmanifest` — makes it installable
- `sw.js` — service worker, enables offline use
- `icon-192.png`, `icon-512.png` — app icons

Keep all files together in the **same folder / repo root**.

## Put it on GitHub Pages (free)
1. Create a new GitHub repository (e.g. `work-flow-assist`).
2. Upload all the files above into the repository root.
3. Go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Pick branch `main` and folder `/ (root)`, then **Save**.
6. After a minute, your app is live at
   `https://YOUR-USERNAME.github.io/REPO-NAME/`.

## Use it offline on phone & laptop
1. Open the GitHub Pages link **once while online**. The service worker caches
   everything.
2. Install it:
   - **iPhone/iPad (Safari):** Share → *Add to Home Screen*.
   - **Android (Chrome):** menu → *Install app* / *Add to Home screen*.
   - **Laptop (Chrome/Edge):** install icon in the address bar.
3. After that it opens like a normal app and works without Wi-Fi or data.

## Where your data lives
Tasks are saved in your browser's local storage on each device. It stays
between sessions, but it is **per-device** — data does not sync across phone and
laptop, and clearing browser data will remove it. (Cross-device sync would need
a backend, which GitHub Pages alone can't provide — say the word if you want to
explore that later.)

> Note: in the Claude in-chat preview, saving may be blocked by the sandbox, so
> it falls back to in-memory (resets on reload). On GitHub Pages or when you open
> `index.html` directly in your own browser, saving works normally.

## Optional: Google Tasks two-way sync
The app can sync tasks with Google Tasks (which also appear in Google Calendar's
Tasks panel). Checking off or deleting a task on either side syncs on your next
sync. Everything lives in a dedicated Google list called **Work Flow Assist**,
so your other Google tasks are left alone.

This part needs a connection and a one-time Google setup (your own account):
1. In the [Google Cloud Console](https://console.cloud.google.com/) create a project.
2. APIs & Services → Library → enable **Google Tasks API**.
3. Configure the OAuth consent screen (External) and add your Google account under **Test users**.
4. Create an **OAuth Client ID** of type **Web application**. Under *Authorized
   JavaScript origins*, add your app's address (e.g. `https://YOU.github.io`, or
   `http://localhost:8000` if testing locally). Note: opening the file directly
   as `file://` will not work for Google sign-in — it must be a real origin.
5. Copy the Client ID, open the app, click the sync (cloud) button in the header,
   paste it, and click **Connect Google**.

Notes: sign-in gives short-lived access, so occasionally you'll reconnect. Sync
is manual (the **Sync now** button) and requires internet; the rest of the app
still works offline.

## Assistant chat (Guide + AI Copilot)
The header's chat button opens an assistant with two tabs:
- **Guide** — a built-in help assistant. Free, offline, instant. Ask how any
  feature works (planning, priorities, the estimator, Gantt, Google sync, etc.).
- **AI Copilot** — a real language model that reasons about your actual tasks in
  plain English ("what should I focus on today?", "reorganize my week"). This
  needs internet and your own Anthropic API key (from console.anthropic.com),
  stored only on your device. Each message costs a small amount against your key,
  and your task list is sent to Anthropic to answer. The default model is Haiku
  (cheapest); you can change it in state if you want a stronger model.
