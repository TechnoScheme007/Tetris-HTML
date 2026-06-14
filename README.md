# Tetris

A polished, classic-faithful Tetris built as a **single HTML file** — no build step, no dependencies, no framework. Open it in a browser and play. Drop it on GitHub Pages and share a link.

It implements the mechanics people expect from modern guideline Tetris: a 7-bag randomizer, ghost piece, hold queue, wall kicks, lock delay, T-spin detection, combos, back-to-back bonuses, and 15 accelerating levels — wrapped in a clean neon presentation with particle effects and clear-type callouts.

## Features

- **15 levels of escalating speed.** Gravity steps from 800 ms per row at level 1 down to 40 ms at level 15. You advance one level every 10 lines.
- **All 7 tetrominoes** (I, O, T, S, Z, J, L) in the standard guideline colors, rendered as beveled "plastic" blocks.
- **Ghost piece** showing exactly where a hard drop will land.
- **Hold / swap** slot and a **3-deep Next queue**.
- **7-bag randomizer** so you never get long droughts of the same piece.
- **DAS / ARR movement** — hold left or right for smooth auto-shift.
- **Wall kicks** so pieces rotate against walls and the floor, plus a short **lock delay** for last-moment nudges.
- **Guideline-style scoring** with **T-spin detection** (3-corner rule), **combos**, and **back-to-back** bonuses.
- **Visual juice:** clear-type callouts (Single / Double / Triple / Tetris / T-Spin), combo and back-to-back banners, floating point popups, particle bursts, row flashes, a level-up flash, and a brief screen shake on big clears.
- **Responsive + mobile controls** with on-screen buttons.
- **Accessible:** keyboard focusable, visible focus, and `prefers-reduced-motion` respected (text callouts stay, motion effects switch off).

## Controls

| Action | Key |
| --- | --- |
| Move left / right | `←` / `→` (hold to auto-shift) |
| Rotate clockwise | `↑` |
| Soft drop | `↓` |
| Hard drop | `Space` |
| Hold / swap piece | `Left Shift` |
| Pause / resume | `P` or `Esc` |
| Start / restart | `Enter` |

On touch devices, an on-screen control pad (move, rotate, soft drop, drop) appears below the board.

## Running it

It's one self-contained file. Pick whichever is easiest:

**Just open it.** Double-click `tetris.html` to run it straight from your file system.

**Serve it locally** (recommended so the web fonts load reliably):

```bash
# Python 3
python3 -m http.server 8000
# then visit http://localhost:8000/tetris.html
```

**Publish on GitHub Pages.** Rename the file to `index.html`, push it, then enable Pages under **Settings → Pages** (deploy from the `main` branch, root folder). Your game will be live at `https://<your-username>.github.io/<repo-name>/`.

> The only external resource is two Google Fonts (Press Start 2P and Chivo Mono). If they're blocked, the game falls back to system fonts and still plays fine.

## How scoring works

Line clears are multiplied by your current level:

| Clear | Base points |
| --- | --- |
| Single | 100 |
| Double | 300 |
| Triple | 500 |
| Tetris | 800 |
| T-Spin (no lines) | 400 |
| T-Spin Single | 800 |
| T-Spin Double | 1200 |
| T-Spin Triple | 1600 |

On top of the base:

- **Back-to-back** — chaining "difficult" clears (a Tetris or any T-spin line clear) multiplies the base by **1.5×**.
- **Combo** — clearing lines on consecutive pieces adds **50 × combo × level**.
- **Soft drop** — `+1` per cell.
- **Hard drop** — `+2` per cell.

## Levels and goal

You start at level 1 and gain a level every 10 lines, up to level 15. Each level drops faster than the last. Clearing all 15 levels' worth of lines (150 total) shows a win screen — and you can keep going endlessly at max speed.

## Project structure

```
.
├── tetris.html   # the entire game (HTML + CSS + JS)
└── README.md
```

Everything lives in `tetris.html`: markup, styles, and the game logic in a single inline `<script>`. The playfield and the Hold/Next previews are drawn on `<canvas>` elements.

## Customizing the game

The tunable values are grouped as constants near the top of the script in `tetris.html`:

| Constant | What it controls |
| --- | --- |
| `COLS`, `ROWS` | Board dimensions (default 10 × 20) |
| `CELL` | Block size in pixels |
| `SPEEDS` | Array of gravity intervals (ms per row) for levels 1–15 |
| `LINES_PER_LEVEL` | Lines needed to advance a level (default 10) |
| `MAX_LEVEL` | Top level (default 15) |
| `LOCK_DELAY` | Grounded time before a piece locks |
| `SOFT_INTERVAL` | Soft-drop speed |
| `DAS`, `ARR` | Auto-shift delay and repeat rate |

Want it faster, slower, taller, or a different number of levels? Edit those values — for example, swap in your own `SPEEDS` array to redesign the difficulty curve. Piece colors live in the `PIECES` object.

## Browser support

Works in any modern desktop or mobile browser with `<canvas>` support (Chrome, Firefox, Safari, Edge). No transpiler needed.

## Contributing

Issues and pull requests are welcome. Because it's a single file, changes are easy to review — keep additions dependency-free so the "open and play" promise holds.

Ideas that fit the project:

- A sound layer (move/rotate blips, a clear sound, a Tetris boom)
- A visible row-collapse animation
- Persistent high scores
- A counter-clockwise rotate key

> **Note:** *Tetris* is a registered trademark of The Tetris Company. This project is a personal, non-commercial homage to the classic game and isn't affiliated with or endorsed by the trademark holder. Keep that in mind before distributing it under the Tetris name.
