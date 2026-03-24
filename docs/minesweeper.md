# Minesweeper

Minesweeper is a grid-based puzzle game where the goal is to reveal all safe cells without clicking on any bombs.

- The grid contains hidden bombs
- Each revealed cell shows a number indicating how many bombs are adjacent (including diagonals)
- The player must determine where bombs are located based on these numbers
- The game ends when all safe cells are revealed or a bomb is clicked

[You can play it here](https://cardgames.io/minesweeper/) <br/>

There is no step-by-step for this task but I have given you some sections of code below as a launch point if you are stuck.<br/>
- Ideally your implementation should:
    - Generate a grid with randomly place bombs
    - Allow a user to guess a grid coordinate (Similar to battleship)
    - Check if that grid is a bomb (end the game if it is)
    - If not, reveal the number of adjacent bombs to that cell
<br/>
---

## Some Basic code
You may find some of this code useful as a starting off point...

### 1. Create Grid
```python
gridSize = 5
grid = [[0 for _ in range(gridSize)] for _ in range(gridSize)]
```
---

### 2. Directions (8 surrounding cells)
These directions could be paired with the code below (#3) or using your own implementation
```python
directions = [
    (-1, -1), (-1, 0), (-1, 1),
    (0, -1),           (0, 1),
    (1, -1),  (1, 0),  (1, 1)
]
```
---

### 3. Update Counts

Paired with the directions above, this code checks the grid surrounding a given point, updating the count for that square depending on the number of bombs

```python
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
```
---

### 4. Place Bombs
```python
import random

def place_bombs(num_bombs=5):
    placed = 0
    while placed < num_bombs:
        i = random.randint(0, gridSize - 1)
        j = random.randint(0, gridSize - 1)

        if grid[i][j] != -1:
            grid[i][j] = -1
            placed += 1
```
---

### 5. Showing the grid
Similar to how we did it in battleship
```python
def showGrid():
    for row in grid:
        print(" ".join(str(cell) for cell in row))
```
---