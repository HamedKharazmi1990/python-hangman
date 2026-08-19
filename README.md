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

## 🧠 Problem-Solving Approach

Instead of trying to build the entire game at once, I am breaking the problem down into smaller, manageable steps.

The development process starts with understanding the game logic and designing the program flow before writing the implementation.

---

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

---

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

## 📚 Python Concepts Practiced

This project is designed to reinforce several Python concepts:

* `for` loops
* `while` loops
* `if / elif / else` statements
* Lists
* Strings
* `range()`
* Modules
* Variables and data types
* User input
* Randomization
* Program flow and conditional logic

---

## 🚀 Project Status

🚧 **In Progress**

The project is being developed step by step, with each stage focusing on a specific programming concept or problem-solving task.

---

## 🎯 Learning Goal

The main goal of this project is not only to create a working game, but also to practice a structured approach to problem solving:

**Understand → Break down → Design → Implement → Test → Improve**

The development process and decisions will be documented as the project progresses.

---

## 📁 Project Structure

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
