# Python Hangman 🎯

A simple command-line Hangman game built with Python.

This project is part of my Python learning journey and focuses on applying programming fundamentals through a complete game project.

## 🎮 What I'm Building

The goal is to build a command-line version of the classic **Hangman** game.

The game randomly selects a word, and the player has to guess the word one letter at a time.

For every incorrect guess, the player loses a life and another part of the Hangman is drawn.

The goal is to guess all the letters in the word before running out of lives.

---

# 🧠 Problem-Solving Approach

Instead of trying to build the entire game at once, I am breaking the problem down into smaller, manageable steps.

The development process starts with understanding the game logic and designing the program flow before implementing each part.

## Step 1 — Understanding the Game

The first step was to understand the rules and define what the final program should do.

The game needs to:

- Generate a random word
- Hide the letters from the player
- Allow the player to guess one letter at a time
- Reveal correctly guessed letters
- Remove a life for incorrect guesses
- Draw the Hangman as lives are lost
- Detect when the player wins
- Detect when the player runs out of lives

## Step 2 — Breaking the Problem Down

Before writing code, I broke the game into smaller problems and mapped the program logic using a flowchart.

### 🔍 Game Logic

The program follows this general flow:

1. Generate a random word.
2. Create a hidden representation of the word using blanks.
3. Ask the player to guess a letter.
4. Check whether the guessed letter exists in the word.
5. If the guess is correct:
   - Reveal the corresponding letter(s).
   - Check whether all letters have been guessed.
6. If the guess is incorrect:
   - Remove one life.
   - Add the next stage of the Hangman drawing.
   - Check whether the player has run out of lives.
7. If all letters are revealed, the player wins.
8. If all lives are lost, the player loses.
9. Otherwise, continue asking for another guess.

### 📊 Flowchart

I created a flowchart to visualize the complete logic of the game before starting the implementation.

[View the Hangman Flowchart](assets/hangman-flowchart.pdf)

The flowchart acts as the blueprint for the implementation and helps keep the different game states and exit conditions clear.

---

# 💻 Implementation

## Step 1 — Picking a Random Word and Checking the Answer

With the game flow defined, the first implementation step focused on selecting a random word and checking the player's guess.

### 🎯 1. Select a Random Word

The game needs a word for the player to guess.

Instead of selecting the word manually, I used Python's `random` module to randomly select one word from a predefined list.

The selected word is stored in a variable called `chosen_word`.

This makes each run of the program capable of starting with a different word.

### ⌨️ 2. Get the Player's Guess

Next, the program asks the player to enter a letter.

The input is converted to lowercase so that uppercase and lowercase guesses are handled consistently.

For example:

    Guess a letter: A

becomes:

    a

This makes comparisons easier because the words in the word list are also stored in lowercase.

### 🔍 3. Check the Guess

The next task is checking whether the guessed letter exists in the selected word.

Since a string is a sequence of characters in Python, I used a `for` loop to iterate through each character of the selected word.

For each character, the program compares it with the player's guess:

- If the letters match → `Right`
- If they don't match → `Wrong`

For example, if the selected word is:

    camel

and the player guesses:

    a

the program checks each character:

    c → Wrong
    a → Right
    m → Wrong
    e → Wrong
    l → Wrong

### 🧠 Problem-Solving Breakdown

At this stage, the problem can be reduced to three smaller tasks:

    Random word
         ↓
    Get user's guess
         ↓
    Loop through the word
         ↓
    Compare each letter with the guess
         ↓
    Right / Wrong

Breaking the problem into these smaller steps made it easier to implement and test each part independently.

### 📚 Python Concepts Practiced

- Importing modules
- `random.choice()`
- Variables
- `input()`
- `.lower()`
- `for` loops
- Iterating through strings
- `if / else` statements
- String comparison

---

## Step 2 — Replacing Blanks with Guesses

The next challenge was to move from simply checking whether a guessed letter exists to actually **displaying the current state of the word**.

The player should not see the original word. Instead, they should see a series of blanks representing the letters they still need to guess.

### 🎯 1. Create the Placeholder

First, I created a placeholder containing one underscore for every character in the chosen word.

For example, if the selected word is:

    apple

the player should initially see:

    _ _ _ _ _

The number of blanks is determined dynamically based on the length of the selected word.

This means the same logic works regardless of which word is randomly selected.

### 🔍 2. Build the Display

The next problem was to replace the appropriate blanks with letters that the player has already guessed correctly.

For example, if the selected word is:

    apple

and the player guesses:

    p

the display should become:

    _ p p _ _

To achieve this, I loop through each letter of the chosen word and compare it with the player's guess.

For each position:

- If the current letter matches the guess → add that letter to `display`
- Otherwise → add `_`

This creates a new string representing the current state of the word.

### 🧠 Problem-Solving Breakdown

The logic can be simplified to:

    Get chosen word
          ↓
    Create blanks based on word length
          ↓
    Get user's guess
          ↓
    Loop through each letter
          ↓
    Does the letter match the guess?
          ├── Yes → Add the letter
          └── No  → Add "_"
          ↓
    Display the result

This step builds the foundation for keeping track of the player's progress throughout the game.

### 📚 Python Concepts Practiced

- `len()`
- `range()`
- `for` loops
- Strings
- String concatenation with `+=`
- Variables
- Conditional statements
- Working with character positions

### 💡 Key Learning

The important concept in this step was learning how to **build a new string step by step** based on the contents of another string.

Instead of modifying the original word, the program creates a separate `display` value that represents what the player is currently allowed to see.

---

## Step 3 — Checking if the Player Has Won

At this stage, the game becomes interactive and allows the player to keep guessing until the word has been completely revealed.

The main challenges in this step were:

- Allowing the player to make multiple guesses
- Keeping previously correct guesses
- Detecting when all letters have been guessed
- Knowing when the game should stop

### 🔄 1. Allow Multiple Guesses

The previous version of the game only allowed the player to make one guess.

To allow the player to continue guessing, I introduced a `while` loop.

The loop continues running while the game is not over:

    Game starts
        ↓
    Player makes a guess
        ↓
    Update the display
        ↓
    Are all letters revealed?
        ├── No → Ask for another guess
        └── Yes → Game Over → You Win 🎉

A `game_over` variable is used to control when the loop should stop.

Initially:

    game_over = False

Once all letters have been guessed:

    game_over = True

This provides a clear exit condition for the `while` loop and prevents the program from running indefinitely.

### 🏆 2. Check if the Player Has Won

The `display` string contains underscores for letters that have not been guessed yet.

Therefore, if there are no underscores left in `display`, all letters have been revealed and the player wins.

Conceptually:

    Are there any "_" characters left?
            ↓
        ┌── Yes ──→ Continue playing
        │
        └── No ───→ You Win 🎉

This gives the program its first actual win condition.

### 💾 3. Keep Previous Correct Guesses

While implementing the `while` loop, I encountered an important problem.

Each new guess was rebuilding the `display` string from scratch, which caused previously correct guesses to disappear.

For example:

    First guess: a
    _ a _ _ _

    Second guess: r
    _ _ r _ _

The previous correct guess was lost.

The problem was that the program only knew about the **current guess**, not the guesses that had already been confirmed as correct.

### 🧩 Solution: Store Correct Letters

To solve this problem, I introduced a list called `correct_letters`.

Whenever the player correctly guesses a letter, that letter is added to the list.

The list is created **outside the `while` loop**, so its contents persist between guesses.

    correct_letters = []

When rebuilding the display, the program checks:

1. Is the current letter equal to the player's current guess?
2. Has the current letter already been added to `correct_letters`?

If either condition is true, the letter is revealed.

Otherwise, an underscore is displayed.

### 🧠 Problem-Solving Insight

This step introduced an important programming concept:

> **Maintaining state between iterations of a loop.**

The `correct_letters` list acts as a persistent record of the player's progress.

This allows the program to remember previous correct guesses while continuing to process new guesses.

### 📚 Python Concepts Practiced

- `while` loops
- Boolean variables
- `True` / `False`
- `if / elif / else`
- The `in` operator
- Lists
- `.append()`
- Maintaining state between loop iterations
- Loop exit conditions
- Building strings dynamically

### 💡 Key Learning

The biggest lesson from this step was understanding that a loop can repeatedly execute code while still maintaining information from previous iterations.

By storing correct guesses in a separate list, the program can remember the player's progress and determine when the word has been completely revealed.

---

# 📚 Python Concepts Practiced

Throughout the project, I am practicing:

- Variables and data types
- User input
- `if / elif / else` statements
- `for` loops
- `while` loops
- Lists
- Strings
- `len()`
- `range()`
- Modules
- `random.choice()`
- String concatenation
- `.append()`
- Boolean values
- The `in` operator
- Program flow
- Conditional logic
- Maintaining state
- Problem decomposition

---

# 🚀 Project Status

🚧 **In Progress**

The project is being developed step by step, with each stage focusing on a specific programming concept or problem-solving task.

### Completed

- [x] Understand the game requirements
- [x] Break down the problem
- [x] Create the game flowchart
- [x] Select a random word
- [x] Get and normalize the player's guess
- [x] Check whether the guessed letter exists in the word
- [x] Create placeholders for the hidden word
- [x] Reveal correctly guessed letters
- [x] Allow the player to make multiple guesses
- [x] Keep track of previously correct guesses
- [x] Implement the win condition
- [x] Add a game-over state

### Upcoming

- [ ] Implement the lives system
- [ ] Add the Hangman stages
- [ ] Implement the lose condition
- [ ] Handle repeated guesses
- [ ] Final testing and cleanup

---

# 🎯 Learning Goal

The main goal of this project is not only to create a working game, but also to practice a structured approach to problem solving:

**Understand → Break down → Design → Implement → Test → Improve**

The development process and decisions are being documented as the project progresses.

---

# 📁 Project Structure

    python-hangman/
    │
    ├── assets/
    │   └── hangman-flowchart.pdf
    │
    ├── main.py
    ├── README.md
    └── .gitignore