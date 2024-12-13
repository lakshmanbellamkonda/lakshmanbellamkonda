import random

# List of words to choose from
words = ['python', 'hangman', 'programming', 'developer', 'computer', 'algorithm', 'data', 'science']

# Function to choose a random word
def choose_word():
    return random.choice(words)

# Function to display the current state of the word
def display_word(word, guessed_letters):
    return ''.join([letter if letter in guessed_letters else '_' for letter in word])

# Function to play the Hangman game
def play_hangman():
    word = choose_word()
    guessed_letters = set()
    incorrect_guesses = 0
    max_incorrect_guesses = 6  # Limit on incorrect guesses

    print("Welcome to Hangman!")
    print("You have", max_incorrect_guesses, "incorrect guesses allowed.")

    # Game loop
    while incorrect_guesses < max_incorrect_guesses:
        print("\nCurrent word: ", display_word(word, guessed_letters))
        print("Guessed letters:", ' '.join(sorted(guessed_letters)))
        print(f"Incorrect guesses left: {max_incorrect_guesses - incorrect_guesses}")

        guess = input("Guess a letter: ").lower()

        # Input validation
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a valid letter.")
            continue

        # Check if letter has already been guessed
        if guess in guessed_letters:
            print("You already guessed that letter.")
            continue

        # Add the guessed letter to the set of guessed letters
        guessed_letters.add(guess)

        # Check if the guess is correct
        if guess in word:
            print("Good guess!")
        else:
            print(f"Oops! '{guess}' is not in the word.")
            incorrect_guesses += 1

        # Check if the word is fully guessed
        if all(letter in guessed_letters for letter in word):
            print("\nCongratulations! You've guessed the word:", word)
            break
    else:
        print("\nGame Over! You've used all your incorrect guesses.")
        print(f"The word was: {word}")

# Start the game
if __name__ == "__main__":
    play_hangman()
