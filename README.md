# voiceit

A static web app that reads Hebrew text aloud. Paste text, hit play, and listen.

**Live demo:** https://ronmailx-boop.github.io/voiceit/

## Features

- **Paste & speak** - paste Hebrew text into the box and click the play button to hear it read aloud, using the browser's built-in Web Speech API (`he-IL`).
- **Pause / Resume** - stop mid-sentence and continue from the same spot. Implemented by canceling and re-speaking from the last known position rather than the browser's native `pause()`/`resume()`, which is unreliable across browsers.
- **Word-by-word highlighting** - the word currently being spoken is highlighted in sync with the audio. Uses real `onboundary` word-boundary events where the browser/voice supports them, falling back to an estimated, timer-driven highlight when they don't.
- **Voice & speed controls** - pick from any installed Hebrew voice and adjust the speaking rate.
- **Installable (PWA)** - can be added to your home screen / installed as an app via the browser's install prompt.

## Tech stack

Plain HTML, CSS, and JavaScript - no build step, no framework, no npm dependencies. Styling via Tailwind CSS (loaded from a CDN). Speech is handled entirely client-side by the browser's Web Speech API.

## Files

| File | Purpose |
|---|---|
| `index.html` | The app itself - UI, styling, and all logic |
| `voiceit-manifest.json` | PWA manifest (name, icons, install behavior) |
| `sw.js` | Service worker (required for installability) |
| `voiceit-icon.png` | App icon / favicon |

## Running locally

Just open `index.html` directly in a browser, or serve the folder with any static file server, e.g.:

```bash
python3 -m http.server
```

## Known limitations

- Hebrew voice availability and quality vary by browser and operating system.
- Word highlighting is exact when the browser fires `onboundary` events, but only approximate (timer-based) on browsers/voices that don't support them.
