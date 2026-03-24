# Simple Guessing Game

We are going to build a simple number guessing game!

## Defining the basics
Every guessing game needs a number to guess. We want to make this random so that each game is different.<br/>
Start by adding this line to the top of your code
```python
import random
```
This makes use of Python's random library, which allows us (amongst other functions) to generate random numbers in a given range.

I recommend reading [this guide](https://www.w3schools.com/python/module_random.asp) on how we can use it to generate a random number.<br/>
Remember to assign this to a variable so we can use it later!

<details>
<summary>Possible Answer</summary>

```python
randomNumber = random.randint(1, 10)
```
Choose any range you want - I've chosen 1-10 so it doesn't take too long to play
</details>

We also want to define a 'user guess' variable so that we can keep track of what the user has guessed, and check it against the random number.</br>

<details>
<summary>Possible Answer</summary>

```python
userGuess = None
```
You can either define this as `None` like I have OR you can set it to take user input: `userGuess = int(input("Enter a guess: "))`. Either method is fine.
</details>

## Game loop
Ok now we have the number chosen we can move onto the game loop.</br></br>

We need to start by defining the conditions we want the loop to run under.<br/>
Have a think about what these could be - why might we stop the loop?

<details>
<summary>Answer</summary>
We want the loop to run while the player has not successfully guessed the number
</details>

We can then turn this into a loop

<details>
<summary>Answer</summary>
```python
while userGuess != randomNumber:
```
Don't forget the colon at the end!
</details>

Now we need to take the user's guess and compare it against the random number.<br/>
You could also print out some messages (ie 'higher' or 'lower') to help guide the user.

<details>
<summary>Possible Answer</summary>
```python
userGuess = int(input("Enter a guess: "))

if userGuess > randomNumber:
    print("Incorrect - go lower")
elif userGuess < randomNumber:
    print("Incorrect - go higher")
else:
    print("Correct!")
```
Remember to convert the user's guess into an integer - we can't compare it to the randomNumber otherwise!
</details>

### Wrapping up
You should now have a very basic number guessing game, congrats!<br/>
Could you add guess tracking, so the player knows how many guesses it took?s<br/>
Can you think of ways to extend this to make it harder/more exciting for the player?<br/><br/>

If you want more of a challenge [try hangman](/hangman)


### Full Code
<details>
<summary>Full Code</summary>
```python
import random

randomNumber = random.randint(1, 10)

userGuess = None

while userGuess != randomNumber:

    userGuess = int(input("Enter a guess: "))

    if userGuess > randomNumber:
        print("Incorrect - go lower")
    elif userGuess < randomNumber:
        print("Incorrect - go higher")
    else:
        print("Correct!")
```
</details