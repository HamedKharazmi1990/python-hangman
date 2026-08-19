# Python Hangman 🎯

A simple command-line Hangman game built with Python.

This project is part of my Python learning journey and focuses on applying programming fundamentals through a complete game project.

## 🎮 What I'm Building

The goal is to build a command-line version of the classic **Hangman** game.

The game randomly selects a word, and the player has to guess the word one letter at a time.

For every incorrect guess, the player loses a life and another part of the Hangman is drawn.

The goal is to guess all the letters in the word before running out of lives.

### Example

```text
Word: _ _ _ _ _ _

Guess a letter: a

Correct!

Word: _ a _ _ _ _

Guess a letter: z

Wrong guess!

Lives remaining: 5
```

---

# 🧠 Problem-Solving Approach

Instead of trying to build the entire game at once, I am breaking the problem down into smaller, manageable steps.

The development process starts with understanding the game logic and designing the program flow before implementing each part.

## Step 1 — Understanding the Game

The first step was to understand the rules and define what the final program should do.

The game needs to:

* Generate a random word
* Hide the letters from the player
* Allow the player to guess one letter at a time
* Reveal correctly guessed letters
* Remove a life for incorrect guesses
* Draw the Hangman as lives are lost
* Detect when the player wins
* Detect when the player runs out of lives

## Step 2 — Breaking the Problem Down

Before writing code, I broke the game into smaller problems and mapped the program logic using a flowchart.

### 🔍 Game Logic

The program follows this general flow:

1. Generate a random word.
2. Create a hidden representation of the word using blanks.
3. Ask the player to guess a letter.
4. Check whether the guessed letter exists in the word.
5. If the guess is correct:

   * Reveal the corresponding letter(s).
   * Check whether all letters have been guessed.
6. If the guess is incorrect:

   * Remove one life.
   * Add the next stage of the Hangman drawing.
   * Check whether the player has run out of lives.
7. If all letters are revealed, the player wins.
8. If all lives are lost, the player loses.
9. Otherwise, continue asking for another guess.

### 🧩 Main Decision Points

The flowchart helped identify the key decisions that the program needs to make:

```text
Start
  ↓
Generate random word
  ↓
Create hidden word
  ↓
Ask for a letter
  ↓
Is the letter in the word?
  ├── Yes → Reveal letter
  │           ↓
  │      Are all letters revealed?
  │           ├── Yes → You Win 🎉
  │           └── No  → Guess again
  │
  └── No → Lose a life
              ↓
        Are all lives lost?
              ├── Yes → Game Over 💀
              └── No  → Guess again
```

### 📊 Flowchart

I created a flowchart to visualize the complete logic of the game before starting the implementation.

**[View the Hangman Flowchart (PDF)](assets/hangman-flowchart.pdf)**

The flowchart acts as the blueprint for the implementation and helps keep the different game states and exit conditions clear.

---

# 💻 Implementation

## Step 1 — Picking a Random Word and Checking the Answer

With the game flow defined, the first implementation step focuses on selecting a random word and checking the player's guess.

### 🎯 1. Select a Random Word

The game needs a word for the player to guess.

Instead of selecting the word manually, I used Python's `random` module to randomly select one word from a predefined list.

The selected word is stored in a variable called `chosen_word`.

This makes each run of the program capable of starting with a different word.

### ⌨️ 2. Get the Player's Guess

Next, the program asks the player to enter a letter.

The input is converted to lowercase so that uppercase and lowercase guesses are handled consistently.

For example:

```text
Guess a letter: A
```

becomes:

```text
a
```

This makes comparisons easier because the words in the word list are also stored in lowercase.

### 🔍 3. Check the Guess

The next task is checking whether the guessed letter exists in the selected word.

Since a string is a sequence of characters in Python, I used a `for` loop to iterate through each character of the selected word.

For each character, the program compares it with the player's guess:

* If the letters match → `Right`
* If they don't match → `Wrong`

For example, if the selected word is:

```text
camel
```

and the player guesses:

```text
a
```

the program checks each character:

```text
c → Wrong
a → Right
m → Wrong
e → Wrong
l → Wrong
```

### 🧠 Problem-Solving Breakdown

At this stage, the problem can be reduced to three smaller tasks:

```text
Random word
     ↓
Get user's guess
     ↓
Loop through the word
     ↓
Compare each letter with the guess
     ↓
Right / Wrong
```

Breaking the problem into these smaller steps made it easier to implement and test each part independently.

### 📚 Python Concepts Practiced

* Importing modules
* `random.choice()`
* Variables
* `input()`
* `.lower()`
* `for` loops
* Iterating through strings
* `if / else` statements
* String comparison

### 🧪 Testing

I tested the implementation by:

* Running the program multiple times to verify that different words can be selected.
* Entering both uppercase and lowercase guesses.
* Testing letters that exist in the selected word.
* Testing letters that don't exist in the selected word.

### 💡 Key Learning

The main lesson from this step was learning how several basic Python concepts can work together to solve a larger problem.

A simple combination of `random.choice()`, `input()`, a `for` loop, and `if / else` statements is enough to implement the first piece of the game's logic.

---

# 📚 Python Concepts Practiced

Throughout the project, I will be practicing:

* Variables and data types
* User input
* `if / elif / else` statements
* `for` loops
* `while` loops
* Lists
* Strings
* `range()`
* Modules
* Randomization
* Program flow
* Conditional logic
* Problem decomposition

---

# 🚀 Project Status

🚧 **In Progress**

The project is being developed step by step, with each stage focusing on a specific programming concept or problem-solving task.

### Completed

* [x] Understand the game requirements
* [x] Break down the problem
* [x] Create the game flowchart
* [x] Select a random word
* [x] Get and normalize the player's guess
* [x] Check whether the guessed letter exists in the word

### Upcoming

* [ ] Display the hidden word
* [ ] Track correctly guessed letters
* [ ] Implement the lives system
* [ ] Add the Hangman stages
* [ ] Implement win and lose conditions
* [ ] Handle additional game logic
* [ ] Final testing and cleanup

---

# 🎯 Learning Goal

The main goal of this project is not only to create a working game, but also to practice a structured approach to problem solving:

**Understand → Break down → Design → Implement → Test → Improve**

The development process and decisions are being documented as the project progresses.

---

# 📁 Project Structure

```text
python-hangman/
│
├── assets/
│   └── hangman-flowchart.pdf
│
├── main.py
├── README.md
└── .gitignore
```
