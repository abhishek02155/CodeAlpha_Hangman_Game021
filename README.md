# CodeAlpha_Hangman_Game021
this is a simple text-based Hangman game built as part of the CodeAlpha Python Programming Internship (Task 1).
The player tries to guess a hidden word one letter at a time. Each incorrect guess reduces the number of remaining attempts. The player wins by guessing all the letters in the word before running out of attempts.
Features
Random word selection from a predefined list of 5 words
Maximum of 6 incorrect guesses allowed
Displays the word progress with underscores for unguessed letters
Tracks and displays already guessed letters
Option to play again after each round
Concepts Used
random module for word selection
while loops for game flow
if-else conditional statements
String and list manipulation
Basic input/output handling
"""
CodeAlpha - Python Programming Internship
Task 1: Hangman Game
A simple text-based Hangman game where the 
player guesses a word one letter at a time.
"""

import random

# A small list of predefined words
WORDS = ["python", "hangman", "programming", "internship", "developer"]
MAX_ATTEMPTS = 6

def choose_word():
    """Pick a random word from the word list."""
    return random.choice(WORDS)

def display_word(word, guessed_letters):
    """Return the word with unguessed letters shown as underscores."""
    display = ""
    for letter in word:
        if letter in guessed_letters:
            display += letter + " "
        else:
            display += "_ "
    return display.strip()

def play_hangman():
    word = choose_word()
    guessed_letters = []
    wrong_guesses = 0

    print("=" * 40)
    print("Welcome to Hangman!")
    print(f"You have {MAX_ATTEMPTS} incorrect guesses allowed.")
    print("=" * 40)

    while wrong_guesses < MAX_ATTEMPTS:
        print("\nWord: " + display_word(word, guessed_letters))
        print(f"Wrong guesses: {wrong_guesses}/{MAX_ATTEMPTS}")
        print("Guessed letters:", ", ".join(guessed_letters) if guessed_letters else "None")

        guess = input("Guess a letter: ").lower().strip()

        # Basic input validation
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single valid letter.")
            continue

        if guess in guessed_letters:
            print("You already guessed that letter. Try again.")
            continue

        guessed_letters.append(guess)

        if guess in word:
            print(f"Good job! '{guess}' is in the word.")
            # Check if the player has won
            if all(letter in guessed_letters for letter in word):
                print("\n" + "=" * 40)
                print(f"🎉 Congratulations! You guessed the word: {word}")
                print("=" * 40)
                return
        else:
            wrong_guesses += 1
            print(f"Sorry, '{guess}' is not in the word.")

    # Player ran out of attempts
    print("\n" + "=" * 40)
    print("💀 Game over! You've run out of attempts.")
    print(f"The word was: {word}")
    print("=" * 40)

def main():
    while True:
        play_hangman()
        again = input("\nPlay again? (y/n): ").lower().strip()
        if again != "y":
            print("Thanks for playing. Goodbye!")
            break

if __name__ == "__main__":
    main()
