# Go White Belt Projects

These projects will help you synthesize the concepts from the lessons and daily exercises into complete, working programs.

## Project 1: Simple Command-Line Calculator

**Objective:** Build a command-line tool that performs basic arithmetic. This project will solidify your understanding of variables, control flow, functions, and handling user input.

**Requirements:**

1.  **Read User Input**: The program should prompt the user to enter two numbers and an operator (+, -, *, /).
    *   Hint: Use the `fmt` package (`fmt.Scanln` or `fmt.Scanf`) to read input from the user.
2.  **Perform Calculation**:
    *   Write a function for each operation (e.g., `add(a, b)`, `subtract(a, b)`).
    *   Use an `if/else` or a `switch` statement to call the correct function based on the user's chosen operator.
3.  **Handle Division by Zero**: If the user tries to divide by zero, print an informative error message instead of letting the program crash.
4.  **Print the Result**: Display the result of the calculation in a user-friendly format (e.g., "Result: 10 + 5 = 15").
5.  **Loop (Optional but Recommended)**: Wrap the logic in a `for` loop so the user can perform multiple calculations without restarting the program. Allow them to type "exit" to quit.

**Concepts Reinforced:**
*   Variables and Data Types (`int`, `float64`, `string`)
*   Functions
*   Control Flow (`if/else`, `switch`)
*   Reading user input (`fmt` package)
*   Error handling (division by zero)

## Project 2: Word Counter

**Objective:** Write a program that reads the content of a text file and counts the frequency of each word. This is a classic programming problem that introduces file I/O and data manipulation with maps.

**Requirements:**

1.  **Create a Text File**: Create a simple `input.txt` file with a few sentences of text.
2.  **Read the File**:
    *   Use the `os.ReadFile` function (from the `os` package) to read the entire content of `input.txt` into a string.
    *   Remember to handle the potential error that `ReadFile` can return.
3.  **Process the Text**:
    *   The text will be a single string. You need to split it into individual words.
    *   Hint: Use the `strings.Fields()` function to split the string by whitespace.
    *   Optional: Convert all words to lowercase using `strings.ToLower()` to ensure "The" and "the" are counted as the same word.
4.  **Count the Words**:
    *   Use a map (`map[string]int`) to store the word counts.
    *   Iterate through your slice of words. For each word, increment its corresponding counter in the map.
5.  **Print the Results**:
    *   Iterate over the map and print each word along with its count (e.g., "the: 5", "go: 2").

**Concepts Reinforced:**
*   File I/O (`os.ReadFile`)
*   Error Handling
*   Maps (`map[string]int`)
*   Slices
*   String manipulation (`strings` package)
*   `for...range` loops

Completing these projects will give you a strong, practical foundation in Go and prepare you for more complex challenges. Good luck!
