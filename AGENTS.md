# AGENTS.md

Vanilla HTML5 Canvas Asteroids clone. No dependencies, no bundler, no package.json, no test/lint/build tooling.

## Run / verify
- Open `index.html` directly in the browser, or `npx serve .` then visit http://localhost:3000.
- Verification is browser-only: open the page, check the console for errors. Don't introduce tooling for small changes.

## Codebase facts
- `game.js` is the entire game. It is a classic script loaded via `index.html` `<script src="game.js">`; no `import`/`export`. Adding ES modules requires changing that script tag to `type="module"`.
- `game.js` runs top-level `document` access (lines 3-4) and `requestAnimationFrame` at the bottom; it cannot be executed in Node.
- Canvas must stay in sync with the module constants: `width="800" height="600"` in `index.html` equals `W = 800` / `H = 600` in `game.js`. `wrap()` and all positioning depend on both matching.
- Entity pattern: each class (`Ship`, `Bullet`, `Asteroid`, `Particle`) exposes `update(dt)`, `draw()`, and a `dead` flag; arrays are filtered each frame. `dt` is seconds, clamped to `0.05`; speeds are in px/s.
- Input uses `e.code` (`ArrowLeft`, `Space`, ...) and the handler `preventDefault()`s arrows/space to stop page scrolling.

## Conventions
- UI strings are Spanish (`NIVEL`, `PUNTAJE`, `GAME OVER`). Keep new HUD/overlay text Spanish.
- Code comments are Spanish; file starts with `'use strict'`.

## Gotchas
- README advertises power-ups and a "estrella fugaz" asteroid type that do not exist in `game.js`. The code is the source of truth; fix README or code, don't assume the feature exists.