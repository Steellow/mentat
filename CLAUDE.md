# mentat

- This repo is entirely maintained by AI. Always keep this file up to date about features, architect, plans and such.

## Tech Stack

- Plain HTML/CSS/JavaScript (single file)
- No frameworks or dependencies

## Features

- 1-minute timed mental math game (divider line shrinks as timer)
- Four operations: addition, subtraction, multiplication, division
- Separate difficulty tracking for each operation
- Auto-submit on correct answer (no Enter needed)
- Play again option after game ends
- Stats page with top 10 scores, total puzzles solved, and level details
- Post-game response time analysis with ASCII bar chart
- "New record!" rainbow animation when beating high score

## Difficulty System

- Separate difficulty for all 4 operations (each starts at 1.0, no upper cap)
- All difficulties persisted to localStorage
- Main page shows average level (floor of average of all 4)
- Target answer time: 4 seconds (scales with hard multiplier)
- Smooth scaling based on answer time:
  - Time multiplier = clamp((targetTime - elapsed) / 3, -1, 1)
  - Adjustment = 0.25 * timeMultiplier
- Easy problems never increase difficulty
- Points per correct answer = floor(difficulty) * hardMultiplier

## Number Generation

### Addition/Subtraction
- First number scales with difficulty: min = 1 + floor(diff), max = 5 + floor(diff * 2)
- Second number has wider range: 1 to max (more variability)
- Subtraction generates answer first (minNum to maxNum*2), then constructs num1 = answer + num2

### Multiplication
- Smaller numbers to match addition difficulty: min = 2 + floor(diff/3), max = 4 + floor(diff/2)
- Both numbers use minNum (no trivial ×1 problems)

### Division
- Even smaller numbers (division is cognitively harder): min = 2 + floor(diff/5), max = 3 + floor(diff/3)
- Both answer and divisor use same range (minNum to maxNum)
- Generates answer and divisor, computes dividend (clean integer division)

### Operation Selection
- All 4 operations randomly selected (equal probability)
- Debug mode allows filtering which operations appear
- Same answer never appears twice in a row (regenerates if needed)

### 10% Chance Modifiers (rolled independently)
- Easy problem: uses half current difficulty (minimum 1.0), never increases level
- Hard problem: 2-5x current difficulty, points and target time scale with multiplier
- Three-number problem: adds a third number (addition/subtraction only)
- Challenge multiplier: doubles one random number (addition/subtraction only)
- Round number anchor: replaces one number with 10, 20, 25, 50, or 100 (addition/subtraction only)
- Negative result (subtraction only): answer is a negative number

## Architecture

- `index.html` - Main game with inline JavaScript
- `stats.html` - Stats page (top 10 scores, levels, total puzzles)
- `settings.html` - Settings page (custom key bindings)
- `style.css` - Hacker/arcade dark theme styles
- Two screens in index: main (start), game (toggled via CSS classes)

## Settings

- Custom key bindings for number input (useful without numpad)
- Key bindings stored in localStorage as `keyBindings` object
- Debug mode toggle

## Debug Mode

- Toggle via settings page (stored in localStorage as `debugMode`)
- Shows all 4 operation difficulties
- Shows delta changes with operation indicator
- Shows active modifiers for current puzzle
- Checkboxes to enable/disable each operation type
- Infinite time (no countdown)
- Manual +1/-1 difficulty buttons (affects current operation)
- End Game button
- High scores are NOT saved in debug mode (prevents unfair scores)

## UI Style

- Dark background (#0a0a0a)
- Red accent (#ff3333) with subtle glow effects
- Monospace font throughout (SF Mono, Monaco, etc.)
- Hacker/arcade aesthetic with sharp corners
- Gold high score (#ffd700), orange debug elements