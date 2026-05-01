# Beeper

A simple browser-based interval reminder. Set a duration, pick a sound, walk away — it beeps on schedule. Plays built-in synth sounds out of the box, or your own Spotify tracks if you connect an account.

Single HTML file, no build step, no dependencies (Spotify SDK loads from CDN at runtime).

## Features

- Customizable interval (seconds, minutes, or hours)
- Customizable repetitions (fixed count or infinite)
- 8 built-in sounds generated via Web Audio API (Beep, Chime, Ding, Alarm, Bell, Bloop, Pulse, Digital)
- Optional Spotify integration — search any track, set it as your alarm
- Pixel-art animated background
- Pixelated audio-reactive sound-wave visualizer
- Settings and Spotify login persist across sessions

## Quick start (built-in sounds only)

Just open `beeper.html` in a browser. No setup needed.

## Spotify setup (optional)

Spotify integration requires a Spotify Premium account and your own (free) Spotify Developer app. The app must be served over HTTP — Spotify won't accept `file://` redirect URIs.

### 1. Serve the file locally

In the project folder, run:

```bash
python -m http.server 5173
```

Then open `http://127.0.0.1:5173/beeper.html` in your browser.

(Or deploy to GitHub Pages and use the public URL — see below.)

### 2. Create a Spotify Developer app

1. Go to <https://developer.spotify.com/dashboard> and sign in
2. Click **Create app**
3. Fill in any name and description
4. Set **Redirect URI** to your URL (e.g. `http://127.0.0.1:5173/beeper.html`) and click **Add**
5. Check **Web API** and **Web Playback SDK**
6. Save, then open the app's **Settings** and copy the **Client ID**

### 3. Connect

In the Beeper UI, paste your Client ID into the Spotify section and click **Connect Spotify**. You'll be redirected to authorize, then bounced back. Login is cached in `localStorage` — you won't have to log in again.

## Deploy to GitHub Pages (recommended)

Pages gives you a free public HTTPS URL, which removes the need to run a local server:

1. Push this repo to GitHub
2. In the repo, go to **Settings → Pages**
3. Under **Source**, pick the `main` branch and `/ (root)` folder, then **Save**
4. Wait ~1 minute, then visit `https://<your-username>.github.io/<repo-name>/beeper.html`
5. Add that URL to your Spotify app's Redirect URIs

## Tech notes

- Uses Web Audio API for all built-in sounds and analyser-based visualization
- Spotify uses the Authorization Code with PKCE flow — no client secret needed, all browser-side
- Spotify playback uses the Web Playback SDK (Premium-only)
- During Spotify playback the visualizer uses a synthesized rhythm wave (Spotify SDK audio is sandboxed and can't be analysed directly)

## License

MIT
