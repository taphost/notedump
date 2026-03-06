# LLM Test Prompts — Vanilla JS Games

> **Nota:** tutti i prompt sono ordinati per difficoltà d'esecuzione stimata, dal più semplice al più complesso. Usali per testare una LLM in modalità chat o agente. Single HTML file, vanilla JS, zero librerie.

---

## Sezione A — Vibe Coder

### 1. Snake

> Build me Snake. Single HTML file, vanilla JS, no libraries. The snake moves on a grid, eats food, grows, and dies if it hits a wall or itself. Keyboard arrows to control it. Show the score. Make it look clean — not a tutorial project.

---

### 2. 2048

> Build me 2048. Single HTML file, vanilla JS, no libraries. Arrow keys to slide tiles, same numbers merge, get to 2048 to win. Show the score and a best score that sticks around. Make it feel satisfying to play — smooth, responsive, nice to look at.

---

### 3. Minesweeper

> Build me Minesweeper. Single HTML file, vanilla JS, no libraries. Left click to reveal, right click to flag. Generate the minefield after the first click so you never die immediately. Show how many mines are left and a timer. Let me choose between easy, medium and hard. Make it look sharp, not like Windows 95.

---

### 4. Game of Life

> Build me a Game of Life. Single HTML file, vanilla JS, no libraries. Make the grid fill most of the screen, cells should look alive — not just grey squares. Give me a way to start/stop it, clear it, and randomize it. I want to be able to draw cells with the mouse too. Make it feel cool to look at, not like a university assignment.

---

### 5. Tetris

> Build me Tetris. Single HTML file, vanilla JS, no libraries. Classic pieces, keyboard controls, game over when the stack hits the top. Make it look good — dark, moody, something you'd actually want to stare at. Score goes up when you clear lines. Don't make it ugly.

---

## Sezione B — Spec Driven

### 1. Snake

Build a Snake game. Single HTML file, vanilla JS, no libraries.

- Grid-based movement, fixed tick rate
- Arrow keys or WASD to change direction
- Food spawns randomly on empty cells
- Snake grows on eat, dies on wall or self collision
- Display current score
- Game over screen with restart option

---

### 2. 2048

Build a 2048 game. Single HTML file, vanilla JS, no libraries.

- 4×4 grid, arrow keys to slide all tiles
- Tiles with equal value merge into their sum
- New tile (2 or 4) spawns after each move
- Display score and best score (persist with localStorage)
- Show win state at 2048, allow continuing
- Show game over when no moves remain

---

### 3. Minesweeper

Build Minesweeper. Single HTML file, vanilla JS, no libraries.

- Left click to reveal, right click to flag
- Mine placement happens after first click (safe first move)
- Auto-reveal empty adjacent cells recursively
- Display mine counter and elapsed timer
- Three difficulty presets: easy / medium / hard
- Win state when all non-mine cells are revealed

---

### 4. Game of Life

Build Conway's Game of Life. Single HTML file, vanilla JS, no libraries.

- Grid rendered on `<canvas>`, fills the viewport
- Simulation runs on a configurable interval
- Controls: start/stop, clear, randomize
- Mouse drag to draw/erase cells on the grid
- Cell color distinct from background, non-default palette

---

### 5. Tetris

Build Tetris. Single HTML file, vanilla JS, no libraries.

- All 7 tetrominoes (I, O, T, S, Z, J, L) with correct colors
- Arrow keys to move left/right, up or Z/X to rotate, down to soft drop
- Full lines clear and collapse the stack
- Score increases per lines cleared (more lines = more points)
- Speed increases over time
- Game over when a new piece cannot spawn
- Display score, level and next piece preview
