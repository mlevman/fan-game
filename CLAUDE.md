# Fan Game — Claude Code Instructions

## Project

A 2D side-scrolling platformer in a single HTML file (`index.html`).
A humorous side project, unrelated to the owner's main project (NutrientAI).
Development is iterative: the owner gives tasks, Claude Code implements them.

The hero is a football fan in yellow-and-blue colors. Enemies are generic riot-police types (baton / shield). Arsenal: fist, scarf, urine (stream and bottles), stomp.

Full concept and version history — see `docs/history.md`.

## Tech Stack

- Plain HTML + JS + Canvas 2D.
- No frameworks, libraries, CDNs, or external files.
- Everything in a single `index.html`.
- Audio — synthesized via Web Audio API, no audio files.

## Communication Style

- **Talk to the owner in Russian, formal `вы` form.**
- Owner is a non-technical founder, learning as the project evolves.
- Style: business-like, no filler, no excessive enthusiasm, no emojis.
- For major changes: brief plan first, then the edit.
- Don't suggest introducing external dependencies without asking.
- Never add real trademarks, logos, names, or organizations to the game.

## Workflow

1. Owner states a task.
2. Claude Code plans the change briefly, in Russian.
3. Implements via `str_replace` (preferred) or full rewrite only when necessary.
4. After any JS change, syntax-check:
   `node -e "new Function(require('fs').readFileSync('index.html','utf8').match(/<script>([\s\S]*?)<\/script>/)[1])"`
5. Owner tests in the browser.
6. On approval: `git add . && git commit -m "..."`. Claude suggests the commit message; owner can edit.
7. For complex changes, use intermediate commits — easier to roll back.

## Code Architecture (sections in `index.html`, top to bottom)

1. HTML markup (canvas, HUD, audio panel).
2. Audio system (Web Audio API): SFX generators, music pattern, volume controls.
3. World constants, platforms, enemy and bottle spawns.
4. `player` object with all state fields.
5. Input handling (`keys`, `pressedOnce`, `consumePress`).
6. Physics (`resolvePlatformCollision`, `rectsOverlap`).
7. Update logic (`updatePlayer`, `updateEnemies`, `updateBottles`, `updatePee`, `updateSplashes`, `updateSplatters`, `updateBeers`).
8. Rendering (`drawBackground`, `drawPlatforms`, `drawFan`, `drawEnemy`, `drawBeer`, `drawBottles`, `drawPee`, `drawSplashes`, `drawSplatters`, `drawHUD`).
9. `reset()` and the main `loop()`.

## Fragile Spots — Handle With Care

- **`updatePlayer`** has early `return`s for paralysis states (`pukeTimer`, `fillingTimer`). Order matters: puke first, then filling.
- **Stomp hit** requires all three conditions simultaneously: `vy > 3 && !onGround && comingFromAbove`. Removing any breaks the crouch-stomp bugfix.
- **`peeSound`** is a looping noise node. Must be stopped on death, reset, or any change to the `peeing` flag, or it keeps playing.
- **`peeSegments`** is the array of markers for the HUD urine bar. Must be cleaned both on consumption and when the tank empties.
- **`reset()`** must zero out ALL player fields and arrays. A forgotten field = a post-restart bug.
- **`AudioContext`** starts only on first user interaction (keydown/click/touchstart). Handlers are registered with `{once: true}`.

## Current Constants
Canvas: 900×480
Level length: 4800 px
Ground: y = 420
Player: 34×64 (crouch 34×44), speed 4.2, jump -13.5
Enemy: 36×60
Bottle: 22×42 (world), ~14×22 (HUD icon)
Gravity: 0.7, max vy: 18
Pee tank: 600 max, +180 per beer, -90 per super-bottle fill
Timers: filling 150, puking 120, invuln 45 (frames @ 60fps)
Super-bottle explosion radius: 90 px

## Roadmap (priority order)

1. Touch controls for mobile devices.
2. Start screen and death screen with score.
3. Local high scores (localStorage).
4. Split into 2–3 levels with different themes (street / stadium / night city / metro / police station).
5. Final boss (riot squad commander).
6. Wrap as a Telegram Mini App for distribution.
7. Audio and music polish.

## Distribution

Telegram Mini Apps is the primary channel. Target audience — owner's friends on Telegram. No App Store / Google Play.

Hosting — GitHub Pages (free HTTPS from the same repo).

## Content Rules

- No trademarks or real product names anywhere in the game, including labels, logos, company names.
- Bottle silhouette is intentionally generic (resembles a lager bottle); label uses pseudotext, not real words.
- Enemies are abstract "security forces", not affiliated with any real organization or country.
- The crayfish on the bottle label is a cartoon silhouette, not a copy of any specific brand's artwork.