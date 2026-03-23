## Hangman
We are going to build the game hangman!

### Defining the basics
#### Game Requirements

Every hangman game needs three essential components:

- **Words** - The secret word(s) to guess
- **Letter spaces** - The '_' for unknown letters
- **Hangman figure** - Remaining attempts

#### Fixed Elements

The following remain constant throughout a hangman game:
- The word to be guessed
- The maximum number of incorrect guesses allowed
- The set of available letters to choose from

So we can start by defining these as variables in our code. Remember to choose appropriate names!<br/>
- To make the game more interesting, you will probably want a list of possible words to randomly choose from for each game

<details>
<summary>Possible Answer</summary>

```python
words = [] # Put whatever words you want in here!
```

</details>

We also want to randomly pick a word from the list of words, so that each game is different!<br/>
We therefore need to add this line *at the top of the file*: 
```python
import random
```

Now we can use it to randomly choose a word. I recommend reading 
[this guide](https://www.w3schools.com/python/module_random.asp)
to understand how we can use it. (Have a look at random.choice!)

<details>
<summary>Possible Answer</summary>

```python
selectedWord = random.choice(words)
```
</details>

Finally we want to set a value for number of guesses the player will have before they lose. You can choose this number however you want but I am going for: `number of unique letters + 3`, so they are allowed a few incorrect guesses

<details>
<summary>Possible Answer</summary>
```python
# A couple more guesses then the number of unique letters in the word
numOfGuesses = len(set(selectedWord)) + 3 
```
We didn't cover `set()` in the slides but in this instance it creates a group of unique individual letters from the word<br/>

For example, if the word is "hello", `set(selectedWord)` would give us `{'h', 'e', 'l', 'o'}` with 4 unique letters
</details>

#### Letter Spaces

We want to keep the answer hidden from the user, and show them each individual guess in the correct place so they can work out / guess the others.<br/>

The easiest way to do this is to create a list of '_' <br/>
- The reason we are making a list and not a string will become obvious later!

<details>
<summary>Answer</summary>

```python
visibleWord = ["_"] * len(selectedWord)
```
We can multiply the list here by a value (in this case the length of the word) which will produce a complete list like: `'hello' -> ["_", "_", "_", "_", "_"]`
</details>

### Gameloop
Now we have the basics of the game done - we can move onto the actual loop!

- We want this loop to run under two different conditions:
    - The player still has guesses left
    - The player has NOT guessed the word correctly

We will need to 'join' the visibleWord together, as currently it is a list `["_", "_", ...]` and selectedWord is a word (ie "hello")<br/>
- [Try reading this!](https://www.geeksforgeeks.org/python/python-string-join-method/)

<details>
<summary>Possible Answer</summary>

```python
while "".join(visibleWord) != selectedWord and numOfGuesses > 0:
    ...
```
</details>

Once that is complete, now we need to print out some info to the player</br>
Ideally this should be the number of guesses remaining, and the current visible letters (Use a similar technique to above to make this pretty!)

<details>
<summary>Possible Answer</summary>
```python
print("You have", numOfGuesses, "remaining!")
print(" ".join(visibleWord))
```
</details>

- Finally we need to
    - Take the user's guess
    - Check its valid (ie in the word)
    - Reveal that letter if so!
    - Remove a guess remaining if not
<br/>
Making visibleWord a list will have made this much easier!

<details>
<summary>Possible Answer</summary>

  guess = input("Enter a letter: ")

  for i in range(0, len(selectedWord)):

    if selectedWord[i] == guess:
      visibleWord[i] = guess

  if guess not in selectedWord:
    numOfGuesses -= 1
</details>

### Wrapping up
You could add a message once the loop is complete, congratulating the user if they guessed the word correcly (or haranging them if not!)

<details>
<summary>Possible Answer</summary>

```python
if numOfGuesses == 0:
  print("You lost!")
else:
  print("Congrats!")

```
</details>

Congratulations! You have successfully created hangman in Python! Now why not try making [battleship](/battleship)?

### Full Code
<details>
<summary>Full Code</summary>
```python
import random

words = ["techvision", "enactus", "python"]

selectedWord = random.choice(words)
numOfGuesses = len(set(selectedWord)) + 3

visibleWord = ["_"] * len(selectedWord)

while "".join(visibleWord) != selectedWord and numOfGuesses > 0:
  print("You have", numOfGuesses, "remaining!")
  print(" ".join(visibleWord))

  guess = input("Enter a letter: ")

  for i in range(0, len(selectedWord)):

    if selectedWord[i] == guess:
      visibleWord[i] = guess

  if guess not in selectedWord:
    numOfGuesses -= 1


if numOfGuesses == 0:
  print("You lost!")
else:
  print("Congrats!")
```
</details>
