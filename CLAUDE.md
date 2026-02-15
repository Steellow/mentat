# Daily Mental Math

- This repo is entirely maintained by AI. Always keep this file up to date about features, architect, plans and such.

## Tech Stack

- Plain HTML/CSS/JavaScript (single file)
- No frameworks or dependencies

## Features

- 1-minute timed mental math game (divider line shrinks as timer)
- Random addition and subtraction problems
- Separate difficulty tracking for each operation
- Auto-submit on correct answer (no Enter needed)
- Play again option after game ends
- All-time high score displayed on main page (persisted to localStorage)

## Difficulty System

- Separate difficulty for addition and subtraction (both start at 1.0, no upper cap)
- Both difficulties persisted to localStorage
- Main page shows average level (floor of average)
- Target answer time: 4 seconds
- Smooth scaling based on answer time:
  - Time multiplier = clamp((targetTime - elapsed) / 3, -1, 1)
  - Base adjustment = 0.25 * timeMultiplier
- Difficulty increases only if puzzle was at least 50% of current difficulty
  - Increase scaled by puzzleRatio (harder puzzles = bigger boost)
- Difficulty decreases always apply fully
- Points per correct answer = floor(current operation's difficulty)

## Number Generation

- First number scales with difficulty: min = 1 + floor(diff), max = 5 + floor(diff * 2)
- Second number has wider range: 1 to max (more variability)
- Operation randomly selected (50/50 addition/subtraction)
- Subtraction always larger - smaller (positive result)
- 10% chance modifiers (each rolled independently):
  - Easy problem: use base difficulty (1.0) instead of current
  - Three-number addition (addition only): adds a third number
  - Challenge multiplier: doubles one random number
  - Round number anchor: replaces one number with 10, 20, 25, 50, or 100

## Architecture

- `index.html` - HTML structure and inline JavaScript
- `style.css` - Obsidian-inspired dark theme styles
- Two screens: main (start), game (toggled via CSS classes)

## Debug Mode

- Toggle via `DEBUG` constant in JavaScript
- Shows both addition and subtraction difficulties
- Shows delta changes with operation indicator
- Infinite time (no countdown)
- Manual +1/-1 difficulty buttons (affects current operation)
- End Game button

## UI Style

- Dark background (#1e1e1e)
- Purple accents (#a88bfa)
- Clean, minimal markdown-file aesthetic