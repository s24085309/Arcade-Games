# ♾️ Infinity Arcade — TV

A self-contained, single-file arcade launcher built for a smart TV's browser. No build step, no
dependencies, no server required — `index.html` is the entire app.

Originally built as part of [Home-Dashboard](https://github.com/s24085309/Home-Dashboard)'s
"Infinity Arcade" feature; this repo carries the standalone TV-focused half of that work so it
can be opened directly on a TV without the rest of the dashboard.

## Running it

- **Locally**: open `index.html` in any browser, or serve the folder with anything static
  (`python3 -m http.server`, `npx serve`, etc.) and visit it.
- **On a smart TV**: point the TV's browser at the GitHub Pages URL for this repo (enable Pages
  in *Settings → Pages → Deploy from a branch → main*, or let the included workflow deploy it
  automatically once Pages is set to "GitHub Actions" as the source).

## Features

- **Built-in games**: Tic-Tac-Toe (vs. a simple AI), Memory Match, and Whack-a-Mole — all
  playable immediately, no setup needed.
- **Add your own games**: paste the URL of any self-contained HTML5 game and it's added to
  "Your Games" and saved in the TV's browser storage. Anything that needs a native app, a
  console emulator, or a downloaded ROM can't run in a browser and is called out as
  unsupported rather than faked.
- **D-pad / remote navigation**: arrow keys, Enter, and Escape drive a focus-ring UI that
  covers most TV remotes once the TV's browser maps them to keyboard events.
- **Real Bluetooth controller support** via the standard [Gamepad API](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API),
  polled every frame for D-pad/stick navigation and A/B buttons.

  **Important:** pairing happens in the TV's own Bluetooth settings, not inside this app. The
  browser's Web Bluetooth device-pairing API can't actually drive standard HID game
  controllers (wrong Bluetooth profile) and has poor smart-TV browser support, so there's
  intentionally no in-page "pair" button — it wouldn't work. Pair the controller with the TV
  like you would for anything else; once paired, the browser exposes it automatically through
  the Gamepad API and this app picks it up.
- High scores are saved per built-in/added game in `localStorage`. Custom games that want to
  report a score back can `postMessage({ type: 'infinityArcadeScore', value: <number> }, '*')`
  to the parent window.

## Adding a game

From the home screen, select **ADD GAME**, give it a name, and paste the URL of a
self-contained HTML5 game (one that runs entirely from a single link, with no login and no
separate files it needs to load). It's saved locally on that TV/browser.
