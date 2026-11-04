# Number Guessing Game

This project is the final component of the freeCodeCamp Relational Database Certification. It integrates relational database management with procedural Bash scripting to create an interactive command-line game that tracks user play history, including total games played and personal high scores.

## Project Overview

The objective of this project is to build a number guessing game (`number_guess.sh`) that generates a random number between 1 and 1000 and prompts the user to guess it. The script communicates with a PostgreSQL database to check if the player is new or returning. For returning players, it retrieves and displays their historical statistics; for new players, it creates a clean profile. Upon a successful guess, the game records the performance back into the database.

## Tech Stack & Skills Demonstrated

*   **Database Management:** PostgreSQL
*   **Querying Language:** SQL (Data Definition Language - DDL, Data Manipulation Language - DML, Aggregate Functions)
*   **Automation & Logic:** Bash Scripting (Shell Scripting, WHILE/UNTIL Loops, Conditional Logic)
*   **Concepts Applied:** Relational Database Design, Input Validation (Regex for integer filtering), State Management, and Data Persistence.

## Database Schema & Architecture

The database `number_guess` features a structured relational design to efficiently track user performance:

1.  **`users`**: Stores unique player profiles.
    *   `user_id` (SERIAL, Primary Key)
    *   `username` (VARCHAR, Unique, NOT NULL)
2.  **`games`**: Records the metrics of every completed game session.
    *   `game_id` (SERIAL, Primary Key)
    *   `user_id` (INT, Foreign Key referencing `users`)
    *   `guesses_count` (INT, Tracks the number of attempts taken to guess the correct number)

## How the Script Works

The `number_guess.sh` script executes the following programmatic workflow:
1.  **User Authentication:** Prompts for a username (up to 22 characters). It queries the database to see if the username exists.
    *   *If returning:* It computes and prints their total games played and their best game (minimum number of guesses).
    *   *If new:* It inserts the username into the database and prints a custom welcome message.
2.  **Game Initialization:** Generates a random target number between 1 and 1000 and initializes an attempt counter.
3.  **Gameplay Loop:** Continuously prompts the user for guesses.
    *   Validates that the input is a valid integer using regex. If invalid, it prints an error message but continues tracking the state.
    *   Provides high/low hinting feedback based on the user's input.
4.  **Data Logging:** Once the correct number is guessed, the script prints a victory statement and inserts a new log entry into the `games` table to update the player's history.

## How to Run & Test Locally

To test this game on your local machine, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/guvengokhan
    cd fcc-number-guessing-game
    ```

2.  **Recreate the database:**
    Ensure PostgreSQL is running locally, then rebuild and populate the database using the SQL dump file:
    ```bash
    psql -U postgres < number_guess.sql
    ```

3.  **Make the script executable:**
    ```bash
    chmod +x number_guess.sh
    ```

4.  **Run the application:**
    ```bash
    ./number_guess.sh
    ```

---
*Completed as part of the Relational Database Curriculum on freeCodeCamp.*
