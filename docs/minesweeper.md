# Minesweeper

Minesweeper is a grid-based puzzle game where the goal is to reveal all safe cells without clicking on any bombs.

- The grid contains hidden bombs
- Each revealed cell shows a number indicating how many bombs are adjacent (including diagonals)
- If a cell has 0 adjacent bombs, it can reveal surrounding cells
- The player uses logic to determine where bombs are located
- The game ends when all safe cells are revealed or a bomb is clicked

[You can play it here](https://cardgames.io/minesweeper/)

---

## Some Basic code
You may find some of this code useful as a starting off point...

### 1. Create Grid

gridSize = 5
grid = [[0 for _ in range(gridSize)] for _ in range(gridSize)]

---

### 2. Directions (8 surrounding cells)

directions = [
    (-1, -1), (-1, 0), (-1, 1),
    (0, -1),           (0, 1),
    (1, -1),  (1, 0),  (1, 1)
]

---

### 3. Update Counts (based on your logic)

def update_counts():
    for i in range(gridSize):
        for j in range(gridSize):
            if grid[i][j] == -1:
                continue

            count = 0

            for di, dj in directions:
                new_i = i + di
                new_j = j + dj

                if 0 <= new_i < gridSize and 0 <= new_j < gridSize:
                    if grid[new_i][new_j] == -1:
                        count += 1

            if count > 0:
                grid[i][j] = count

---

### 4. Place Bombs

import random

def place_bombs(num_bombs=5):
    placed = 0
    while placed < num_bombs:
        i = random.randint(0, gridSize - 1)
        j = random.randint(0, gridSize - 1)

        if grid[i][j] != -1:
            grid[i][j] = -1
            placed += 1

---

### 5. Showing the grid
Similar to how we did it in battleship

def showGrid():
    for row in grid:
        print(" ".join(str(cell) for cell in row))

---