# Fan Game

A browser-based 2D side-scrolling platformer. Single HTML file, zero dependencies.

## Play

Open `index.html` in any modern browser. That's it.

For mobile play (coming soon) — will be distributed as a Telegram Mini App.

## Controls

| Key       | Action                          |
|-----------|---------------------------------|
| ← →       | Move                            |
| ↑         | Jump                            |
| ↓         | Crouch                          |
| A         | Punch                           |
| D         | Scarf whip                      |
| S         | Urine stream (hold)             |
| E         | Drink a full beer               |
| Q         | Throw an empty bottle           |
| F         | Fill an empty bottle with urine |
| T         | Throw a super-bottle            |
| R         | Restart                         |

## Gameplay

Play as a football fan fighting your way through waves of riot police using an unconventional arsenal: fists, a scarf whip, stomps, thrown bottles, and a urine stream. Drink beer to restore health and refill your tank. Watch out for non-alcoholic beer — it looks almost identical, but induces vomiting and costs you HP.

## Tech Stack

- Vanilla HTML + JavaScript + Canvas 2D
- Web Audio API for all sound effects and background music (synthesized, no audio files)
- No frameworks, no bundlers, no build step

## Project Structure
fan-game/
├── index.html          # The game
├── CLAUDE.md           # Instructions for Claude Code
├── README.md           # This file
├── docs/
│   └── history.md      # Version history
└── archive/            # Legacy versions kept for reference

## Development

Development happens iteratively with Claude Code. See `CLAUDE.md` for architectural notes, fragile code sections, and the current roadmap.

### Syntax check after JS edits
node -e "new Function(require('fs').readFileSync('index.html','utf8').match(/<script>([\s\S]*?)</script>/)[1])"

## Roadmap

- Touch controls for mobile
- Start / death screens with scoring
- Local high scores
- Multiple levels with distinct themes
- Final boss fight
- Telegram Mini App wrapper

## Status

Work in progress. Single-player, single-level, desktop-only for now.

## License

Private side project. No license granted for redistribution at this time.