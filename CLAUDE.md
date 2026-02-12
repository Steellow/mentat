# Daily Mental Math

- This repo is entirely maintained by AI. Always keep this file up to date about features, architect, plans and such.

## Tech Stack

- Plain HTML/CSS/JavaScript (single file)
- No frameworks or dependencies

## Features

- 30-second timed mental math game
- Random addition problems with adaptive difficulty
- Auto-submit on correct answer (no Enter needed)
- Play again option after game ends

## Difficulty System

- Difficulty ranges from 1.0 to 10.0 (starts at 1.0)
- Target answer time: 4 seconds
- Smooth scaling based on answer time:
  - Time multiplier = clamp((targetTime - elapsed) / 3, -1, 1)
  - Base adjustment = 0.25 * timeMultiplier
- Difficulty increases only if puzzle was at least 50% of current difficulty
  - Increase scaled by puzzleRatio (harder puzzles = bigger boost)
- Difficulty decreases always apply fully
- Number range scales with difficulty:
  - Min: 1 + floor(difficulty)
  - Max: 5 + floor(difficulty * 2)
- Points per correct answer = floor(difficulty)
- 10% chance of easy problem (base difficulty) for variety

## Architecture

- `index.html` - HTML structure and inline JavaScript
- `style.css` - Obsidian-inspired dark theme styles
- Three screens: start, game, end (toggled via CSS classes)

## UI Style

- Dark background (#1e1e1e)
- Purple accents (#a88bfa)
- Clean, minimal markdown-file aesthetic