## Battleships
We are going to build a very simple version of the game battleship. It will be single player against preplaced ships (for simplicity!)

#### Create the grid
First things first we need a grid to play the game on!<br/>
You can start by defining a variable for the grid's size (I called mine 'gridSize'), as well as a variable for the number of enemy ships (ie enemyCount).<br/>
To start with we will make these ships occupy one square of the grid - but later on we can extend our code to handle bigger ships!

<details>
<summary>Answer</summary>

```python
gridSize = 10
enemyCount = 6
```

</details>


Ok now thats done - we can actually create the grid.<br/>
We can use a 2D array for this (a list within a list). There are many ways in python to initialise this, but for this project I recommend nested for loops.<br/>
Make sure you fill this with some sort of placeholder data, anything that makes it clear to you its an 'empty' square (I picked '.')

<details>
<summary>Possible Answer</summary>

```python
grid = []
for i in range(gridSize):
    row = []
    for j in range(gridSize):
        row.append(".")
    grid.append(row)
```

</details>

What does this do? Well we initialised an empty list, then iteratively added a new row of '.' to form a gridSize x gridSize grid.<br/>
If we display this it should look like:<br/>
```python
. . . . .
. . . . .
. . . . .
. . . . .
. . . . .
```
(I picked gridSize = 5)

<details>
<summary>Displaying the grid</summary>
As the grid is made of rows, we can access each of these rows in turn and print them out.<br/>
However, this will result in: `['.', '.', '.', '.', '.']` which is not neat or easy to read.<br/>
We can use `" ".join(['.', '.', '.', '.', '.'])` to convert this into one string neatly
```python
for row in grid:
    print(" ".join(row))
```

</details>

Perfect! Now we have a grid for which we can play our game on - but its pretty bland at the moment.<br/>
Lets add some enemies!<br/><br/>

#### Adding Enemies
For this we probably want to place the enemies randomly - no point having them in the same place each time!
We therefore need to add this line *at the top of the file*: 
```python
import random
```

Now we can use it to generate random numbers. I recommend reading 
[this guide](https://www.w3schools.com/python/module_random.asp)
to understand how we can use it.


<details>
<summary>Possible Answer</summary>

```python
ships_placed = 0
while ships_placed < enemyCount:
    row = random.randint(0, gridSize - 1) # Why do we subtract 1 here?
    col = random.randint(0, gridSize - 1)

    # Only place if the spot is empty
    if grid[row][col] == ".":
        grid[x][y] = 'S' # (or anything that you know to be a ship!)
        ships_placed += 1
```

</details>

#### User guesses
Ok so we have the grid, and the enemies, now we need to take user guesses!<br/>
If you've ever played battleships, usually you don't see the value of a grid square until you 'take the shot'.

What we can do is make another grid (called something like 'visible_grid' or 'user_view' or similar) which will show the results of shots.

<details>
<summary>Possible Answer</summary>

```python
visible_grid = []
for i in range(gridSize):
    row = []
    for j in range(gridSize):
        row.append(".")
    visible_grid.append(row)
```

</details>

We also need to track how many ships are left, so we can make another variable `enemiesRemaining = ???`<br/><br/><br/>

Ok now for the gameloop

##### Gameloop
This loop needs to run continously until there are no enemies remaining

<details>
<summary>Answer</summary>

```python
while enemiesRemaining > 0:
```
</details>

Make sure to show the current grid to the user, so they can choose where to target next!<br/>
*Hint: How could you output the grid neatly?*

Now we take user input!
*Hint: you may have to take x + y inputs seperately*

<details>
<summary>Answer</summary>

```python
user_row = int(input(f"Enter Row (0-{gridSize-1}): "))
user_col = int(input(f"Enter Col (0-{gridSize-1}): "))
```
</details>

- Make sure the input is in-range - you shouldn't be able to fire outside of the grid!

###### Checking for hits
Now we have user input, the underlying grid and the player visible one - we can tie it all together!

There are 3 conditions your code needs to check for
- Hit a ship
- Missed a ship
- Already guessed that square

Make sure to update the visible grid so the player can see!!


<details>
<summary>Possible Answer</summary>
Remember - you can choose how to display hits or misses to the user!
```python
if visible_grid[user_row][user_col] != ".":
        print("Already guessed!")

elif grid[user_row][user_col] == "S":
    print("Hit!")
    visible_grid[user_row][user_col] = "X"
    shipsRemaining -= 1

else:
    print("Miss!")
    visible_grid[user_row][user_col] = "O"
```
</details>


#### Result
You should now have an, albeit very basic, working version of battleship! Congrats!


- You could extend this by
    - Making the ships different lengths
    - Creating players who can take it in turns
    - Playing against some sort of bot

<details>
<summary>Full Code</summary>
```python
import random

gridSize = 10
enemyCount = 6

grid = []
for i in range(gridSize):
    row = []
    for j in range(gridSize):
        row.append(".")
    grid.append(row)


ships_placed = 0
while ships_placed < enemyCount:
    row = random.randint(0, gridSize - 1) # Why do we subtract 1 here?
    col = random.randint(0, gridSize - 1)

    # Only place if the spot is empty
    if grid[row][col] == ".":
        grid[row][col] = 'S' # (or anything that you know to be a ship!)
        ships_placed += 1

visible_grid = []
for i in range(gridSize):
    row = []
    for j in range(gridSize):
        row.append(".")
    visible_grid.append(row)

shipsRemaining = enemyCount

print("=== BATTLESHIP ===")
while shipsRemaining > 0:

    print("\nCurrent grid:")

    for row in visible_grid:
        print(" ".join(row))

    user_row = int(input(f"Enter Row (0-{gridSize-1}): "))
    user_col = int(input(f"Enter Col (0-{gridSize-1}): "))


    if user_row < 0 or user_row >= gridSize or user_col < 0 or user_col >= gridSize:
        print("Out of bounds!")
        continue


    if visible_grid[user_row][user_col] != ".":
        print("Already guessed!")

    elif grid[user_row][user_col] == "S":
        print("Hit!")
        visible_grid[user_row][user_col] = "X"
        shipsRemaining -= 1

    else:
        print("Miss!")
        visible_grid[user_row][user_col] = "O"


print("\nFinal grid:")
for row in visible_grid:
    print(" ".join(row))

print("You sank all the ships!")
```
</details>
