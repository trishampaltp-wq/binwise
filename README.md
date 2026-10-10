# Binwise

**Collect by need. Keep the city moving.**

A standalone React + Vite waste-collection prototype with 24 simulated Kolkata bins, overflow predictions, priority scoring, capacity-aware truck routes, citizen reports, analytics and a city simulation. This export preserves the current Site's application source and styling unchanged.

## Requirements

Node.js 22 or newer with npm and a modern browser. Internet is needed to install dependencies and load the original Google Fonts. No API key, environment file, ChatGPT account, database or backend is required.

## Run locally

Extract the ZIP and open the `binwise` folder (the one containing `package.json`) in VS Code or a terminal.

```sh
npm ci
npm run dev
```

Open the localhost URL printed by Vite. Press Ctrl+C to stop. If using nvm, run `nvm use` first to read `.nvmrc`.

## Test and build

```sh
npm test
npm run build
npm run preview
```

The build creates `dist/`. A prebuilt `dist/` is also included for convenience. Serve it through an HTTP server rather than double-clicking index.html. On Windows with Python installed, `start-demo.bat` serves it on port 8080. On Linux or macOS with Python 3, run `python3 -m http.server 8080 --directory dist`, then open http://localhost:8080.

## Files

- `src/main.jsx`: React application and all five views.
- `src/style.css`: original styling and responsive layout rules.
- `src/engine.js`: synthetic data, predictions, priority scores, routes and simulation.
- `tests/engine.test.mjs`: eight engine tests.
- `docs/architecture.md`: architecture, exact formulas and model limitations.
- `docs/metrics.json`: calculated initial scenario estimates.
- `docs/pitch-kit.md`: pitches, demo instructions and judge Q&A.
- `docs/export-notes.md`: source provenance, assets and export verification.
- `index.html`, `vite.config.js`: normal Vite entry point and configuration.
- `package.json`, `package-lock.json`: dependencies and reproducible installation.
- `.gitignore`, `.nvmrc`: Git exclusions and Node version.
- `dist/`: prebuilt app, ignored by Git.

## Demonstration

1. Inspect the bins on Overview and click a map marker.
2. Generate Smart Collection Route to review stops and the route comparison.
3. Dispatch, advance four hours, and inspect Fleet.
4. Add a missed-collection report for a low-fill bin, then generate another route.
5. Reset to restore the initial state.

The simulation saves state in this browser's localStorage under `binwise-v1`. Each origin has separate state, so the local app starts independently from the hosted Site. Reports remain in the browser.

## Upload to GitHub

Create an empty repository on GitHub, then run these commands from the folder containing `package.json`. Replace the remote URL with your repository URL.

```sh
git init
git add .
git commit -m "Initial Binwise source export"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/binwise.git
git push -u origin main
```

The `.gitignore` excludes node_modules, builds, local environment files and hosting metadata. The lockfile should be committed. No existing Git history, remote credentials or Site identity are included. No open-source licence has been selected; add one if you wish to grant reuse permissions.

## Host independently

Use `npm ci && npm run build` as the build command and `dist` as the publish directory on a static hosting service. Relative asset paths support repository subpaths. The five views switch through React state, so SPA rewrite rules are not required. Uploading a repository does not automatically publish a website; configure GitHub Pages or another host separately.

## Assets and assumptions

The original inline SVG city map and CSS are included. Lucide icons are supplied by the declared npm dependency. DM Sans and Manrope remain loaded from the original Google Fonts stylesheet URL to preserve appearance. Offline, browser sans-serif fallback fonts are used. There are no separate uploaded images, videos or non-exportable application media in this source version.

All bin locations, readings, drivers and historical data are synthetic. The route planner uses a heuristic rather than actual road navigation or a guaranteed optimum. Savings are single-dispatch simulation estimates, not verified field results. No machine-learning model is used. See the architecture document for full limitations.
