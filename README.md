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

Instead of trying to build the entire game at once, I broke the problem down into smaller, manageable steps.

The development process started with understanding the game logic and designing the program flow before implementing each part.

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

The first implementation step focused on selecting a random word and checking the player's guess.

### 🎯 1. Select a Random Word

The game needs a word for the player to guess.

Instead of selecting the word manually, I used Python's `random` module to randomly select one word from a predefined list.

The selected word is stored in a variable called `chosen_word`.

### ⌨️ 2. Get the Player's Guess

The program asks the player to enter a letter.

The input is converted to lowercase so that uppercase and lowercase guesses are handled consistently.

For example:

    Guess a letter: A

becomes:

    a

This makes comparisons easier because the words in the word list are also stored in lowercase.

### 🔍 3. Check the Guess

The program loops through each character of the selected word and compares it with the player's guess.

For each character:

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

The next challenge was to move from simply checking whether a guessed letter exists to actually displaying the current state of the word.

The player should not see the original word. Instead, they should see a series of blanks representing the letters they still need to guess.

### 🎯 1. Create the Placeholder

First, I created a placeholder containing one underscore for every character in the chosen word.

For example:

    apple

becomes:

    _ _ _ _ _

The number of blanks is determined dynamically based on the length of the selected word.

### 🔍 2. Build the Display

The next step was to replace the appropriate blanks with letters that the player has guessed correctly.

For example, if the selected word is:

    apple

and the player guesses:

    p

the display becomes:

    _ p p _ _

The program loops through each letter of the chosen word:

- If the current letter matches the guess → add the letter
- Otherwise → add `_`

This creates a new string representing the current state of the word.

### 📚 Python Concepts Practiced

- `len()`
- `range()`
- `for` loops
- Strings
- String concatenation with `+=`
- Conditional statements
- Building strings dynamically

### 💡 Key Learning

This step demonstrated how to build a new string step by step based on another string instead of modifying the original word.

---

## Step 3 — Checking if the Player Has Won

At this stage, the game becomes interactive and allows the player to keep guessing until the word has been completely revealed.

The main challenges were:

- Allowing multiple guesses
- Keeping previously correct guesses
- Detecting when all letters have been guessed
- Knowing when the game should stop

### 🔄 1. Allow Multiple Guesses

The previous version only allowed one guess.

To allow the player to continue guessing, I introduced a `while` loop.

The loop continues while the game is not over.

A `game_over` variable controls when the loop should stop.

Initially:

    game_over = False

Once all letters have been guessed:

    game_over = True

### 🏆 2. Check if the Player Has Won

The `display` string contains underscores for letters that have not been guessed.

If there are no underscores left in `display`, all letters have been revealed and the player wins.

Conceptually:

    Are there any "_" characters left?
            ↓
        ┌── Yes ──→ Continue playing
        │
        └── No ───→ You Win 🎉

### 💾 3. Keep Previous Correct Guesses

A problem appeared when the player made multiple correct guesses.

Each new guess rebuilt the `display` string and caused previous correct guesses to disappear.

To solve this, I created a list called `correct_letters`.

Whenever the player correctly guesses a letter, that letter is added to the list.

The list is created outside the `while` loop so that its contents persist between guesses.

When rebuilding the display, the program checks:

1. Is the current letter equal to the player's current guess?
2. Has the current letter already been added to `correct_letters`?

If either condition is true, the letter is revealed.

Otherwise, an underscore is displayed.

### 🧠 Problem-Solving Insight

This step introduced an important programming concept:

**Maintaining state between iterations of a loop.**

The `correct_letters` list acts as a persistent record of the player's progress.

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

---

## Step 4 — Keeping Track of the Player's Lives

The next step was to add the lives system and connect it to the Hangman ASCII art.

### ❤️ 1. Initialize the Lives

The player starts with 6 lives.

A variable called `lives` keeps track of the remaining lives.

    lives = 6

Every incorrect guess removes one life.

    6 → 5 → 4 → 3 → 2 → 1 → 0

When lives reach zero, the game ends and the player loses.

### ❌ 2. Handle Incorrect Guesses

The program checks whether the guessed letter exists in the chosen word.

If the guessed letter is not present, the number of lives is reduced by one.

Conceptually:

    Player makes a guess
            ↓
    Is the letter in the word?
        ┌── Yes ──→ Continue
        │
        └── No ───→ Lose 1 life
                        ↓
                  Are lives = 0?
                    ├── No → Continue
                    └── Yes → You Lose

### 💀 3. Implement the Lose Condition

After reducing the number of lives, the program checks whether the player has reached zero lives.

If:

    lives == 0

the game is marked as over and the player receives a `You lose.` message.

### 🎨 4. Add the Hangman ASCII Art

The project contains several ASCII-art stages representing the Hangman at different points in the game.

The stages correspond to the number of remaining lives:

    Lives: 6 → No man
    Lives: 5 → First stage
    Lives: 4 → Second stage
    Lives: 3 → Third stage
    Lives: 2 → Fourth stage
    Lives: 1 → Fifth stage
    Lives: 0 → Complete Hangman

Correct guesses do not change the Hangman.

Incorrect guesses reduce `lives` and display the corresponding Hangman stage.

### 📚 Python Concepts Practiced

- Variables
- Integers
- Arithmetic operators
- `-=`
- `if` statements
- The `not in` operator
- Boolean game states
- Lists
- List indexing
- ASCII art
- Combining program logic with visual output

---

## Step 5 — Improving the User Experience

The final step focused on improving the structure of the project and making the game easier and more enjoyable to use.

The main goals were:

- Separate data from the main game logic
- Practice importing custom modules
- Give the user better feedback
- Handle repeated guesses
- Show the remaining lives
- Improve the win and lose messages
- Add a visual game logo

### 📦 1. Organize the Word List into a Module

Instead of keeping the word list directly inside `main.py`, I moved it into a separate module called `hangman_words.py`.

The word list can then be imported into the main program.

This separates the game logic from the data and makes the project structure cleaner.

### 🎨 2. Organize the Hangman Art into a Module

The Hangman stages were moved into a separate module called `hangman_art.py`.

This module contains:

- The Hangman stages
- The game logo

The main program imports the required elements instead of keeping all of the ASCII art inside `main.py`.

This makes the main game logic easier to read and maintain.

### 🧩 3. Practice Custom Modules

This step provided practical experience with Python modules and different import styles.

For example, a module can be imported directly:

    import hangman_words

Or specific objects can be imported from a module:

    from hangman_words import word_list

Using separate modules helps keep larger programs organized and makes individual components easier to manage.

### 🔁 4. Handle Repeated Guesses

The game now checks whether the player has already guessed a letter.

If the letter is already inside `correct_letters`, the user receives feedback such as:

    You already guessed a

The player does not lose a life for repeating a correct guess.

This makes the game fairer and provides clearer feedback.

### ❌ 5. Give Feedback for Incorrect Guesses

When the player guesses a letter that does not exist in the chosen word, the program tells them exactly what happened.

For example:

    You guessed d, that's not in the word. You lose a life.

This improves the user experience by making the result of each action clear.

### ❤️ 6. Display Remaining Lives

The game now tells the player how many lives they have remaining.

For example:

    4 / 6 lives left

This gives the player a clear indication of their current game state and how close they are to losing.

### 🏆 7. Reveal the Correct Word

If the player loses the game, the program reveals the word they were trying to guess.

For example:

    The word was: python

This prevents the game from ending without explaining the correct answer.

### 🖥️ 8. Add a Game Logo

The Hangman logo is stored in `hangman_art.py` and displayed when the game starts.

This gives the command-line application a more polished appearance.

### 🧠 Problem-Solving Insight

The final step showed that building a program is not only about making the core functionality work.

After the main logic was complete, I improved:

- Code organization
- User feedback
- Readability
- Maintainability
- User experience

This is an important part of software development because a working program can still be improved significantly.

### 📚 Python Concepts Practiced

- Creating custom modules
- `import`
- `from ... import ...`
- Separating data from logic
- Lists
- Conditional logic
- F-strings
- User feedback
- State management
- Code organization
- User experience considerations

---

# 🏁 Final Game Flow

After completing all five steps, the overall game flow is:

    Start Game
        ↓
    Display Hangman Logo
        ↓
    Select Random Word
        ↓
    Create Hidden Word
        ↓
    Player Makes a Guess
        ↓
    Has The Letter Been Guessed Before?
        ├── Yes → Inform User
        │
        └── No
             ↓
        Is Letter In The Word?
             ├── Yes → Reveal Letter
             │
             └── No → Lose One Life
                        ↓
                  Display Hangman Stage
        ↓
    Are All Letters Revealed?
        ├── Yes → You Win 🎉
        │
        └── No
             ↓
    Are There Any Lives Left?
        ├── Yes → Continue
        │
        └── No → You Lose 💀
                    ↓
               Reveal Word
                    ↓
                  End Game

---

# 📚 Python Concepts Practiced

Throughout the project, I practiced:

- Variables and data types
- User input
- `if / elif / else`
- `for` loops
- `while` loops
- Lists
- Strings
- `len()`
- `range()`
- Modules
- Custom modules
- `import`
- `from ... import ...`
- `random.choice()`
- String concatenation
- `.append()`
- Boolean values
- The `in` operator
- The `not in` operator
- List indexing
- F-strings
- ASCII art
- Program flow
- Conditional logic
- Maintaining state
- Problem decomposition
- Code organization
- User experience

---

# 🚀 Project Status

✅ **Completed**

The Hangman game has now been implemented through five development stages.

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
- [x] Implement the lives system
- [x] Reduce lives after incorrect guesses
- [x] Implement the lose condition
- [x] Display Hangman stages based on remaining lives
- [x] Separate the word list into a custom module
- [x] Separate the Hangman art into a custom module
- [x] Add the Hangman logo
- [x] Handle repeated guesses
- [x] Improve feedback for incorrect guesses
- [x] Display remaining lives
- [x] Reveal the correct word when the player loses
- [x] Improve overall user experience

---

# 📁 Project Structure

    python-hangman/
    │
    ├── assets/
    │   └── hangman-flowchart.pdf
    │
    ├── hangman_art.py
    ├── hangman_words.py
    ├── main.py
    ├── README.md
    └── .gitignore

---

# 🎯 Learning Goal

The main goal of this project was not only to create a working game, but to practice a structured approach to problem solving:

**Understand → Break Down → Design → Implement → Test → Improve**

This project helped me practice turning a larger problem into smaller tasks, implementing each part individually, testing the result, and finally improving the code structure and user experience.

---

# 🔮 Possible Future Improvements

Although the core game is complete, there are still many ways it could be improved.

Possible future ideas include:

- Preventing invalid inputs
- Supporting full-word guesses
- Adding difficulty levels
- Keeping score
- Adding multiple rounds
- Adding a replay option
- Improving the command-line interface
- Adding colors to the terminal
- Creating a graphical user interface
- Adding unit tests
- Improving input validation

These improvements could be added later as additional exercises.

---

# 👨‍💻 About This Project

This project is part of my journey to become a more versatile software developer by expanding my Python skills and practicing problem solving through hands-on projects.

The focus of this project is not simply the final game, but the process of understanding a problem, breaking it down, implementing it step by step, and improving the final result.