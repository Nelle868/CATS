# Computer Aided Typing Software (CATS) 🐱⌨️

This repository contains my solution to the **CATS** project from CS 61A.  
It’s a typing-test program that measures speed and accuracy, does smart autocorrect, and even supports multiplayer typing races.

---

## Overview

- **Language:** Python 3  
- **Main file edited:** `cats.py`  
- **Concepts:** Functions, higher-order functions, recursion, dictionaries, lists, and basic data processing.

CATS reads in text, lets a user (or multiple users) type responses, and then analyzes how well and how quickly they typed.

---

## Main Features I Implemented

### Typing Test & Paragraph Selection

- **Paragraph selection (`pick`)**:  
  Chooses which paragraph to display based on a **selection function** (e.g., “topic-related paragraphs only”) and a given index.
- **Topic filtering (`about`)**:  
  Builds a function that checks whether a paragraph is about a given set of topic words (case-insensitive, ignoring punctuation).
- **Accuracy & speed**:  
  - `accuracy`: Compares a user’s typed string to a reference string and returns the percentage of words typed correctly in the right positions.  
  - `wpm`: Computes words per minute based on the number of characters typed and elapsed time.

### Autocorrect & Word Differences

- **Autocorrect (`autocorrect`)**:  
  Given a user word, a list of valid words, a difference function, and a limit:
  - If the user word is already valid, return it.  
  - Otherwise, return the closest dictionary word under the allowed difference `limit`; if none are close enough, keep the original word.
- **Difference functions**:
  - Implemented recursive word-difference functions (e.g., variants like `feline_fixes` / `furry_fixes`, `minimum_mewtations`) that count:
    - Substitutions
    - Insertions
    - Deletions  
  - Each function respects a `limit` to cut off expensive recursion when the difference is already too large.

These functions let the program intelligently guess what word the typist *meant* to type, instead of just flagging it as wrong.

### Multiplayer Typing Race

- **Progress reporting (`report_progress`)**:  
  - Given a player’s typed words, the prompt, and a sending function, computes how many words at the start are correct in order.
  - Returns a progress fraction and sends a result dictionary (with `id` and `progress`) back to the server.
- **Timing data (`time_per_word`)**:  
  - Converts cumulative timestamps for each player into a per-word timing structure.  
  - Each player’s turns into a list of word times, aligned with the same word sequence.
- **Fastest words (`fastest_words`)**:  
  - Determines which player typed each word the fastest.  
  - Returns a list for each player containing the words they typed quicker than anyone else.

These features power a “typing race” mode where multiple players can compete to see who’s fastest on each word.
