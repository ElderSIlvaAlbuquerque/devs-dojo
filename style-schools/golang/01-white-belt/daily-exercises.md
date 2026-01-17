# Go White Belt Daily Exercises

Practice these exercises daily to build muscle memory and a strong foundation in Go.

## Day 1: Variables and Basic Types

1.  **Hello, Go!**:
    *   Write a program that prints "Hello, Go!" to the console.
    *   Compile and run it from your terminal.
2.  **Variable Declaration**:
    *   Declare an integer variable `age` with a value of 30.
    *   Declare a string variable `name` with your name using the short `:=` syntax.
    *   Declare a float variable `price` with a value of 99.99.
    *   Print all these variables to the console with descriptive text.

## Day 2: Functions and Control Flow

1.  **Simple Adder**:
    *   Write a function `add` that takes two integers as arguments and returns their sum.
    *   Call this function from `main` and print the result.
2.  **Even or Odd**:
    *   Write a program that uses an `if/else` statement to determine if a number is even or odd.
    *   Print the result to the console.
3.  **Counting Loop**:
    *   Use a `for` loop to print numbers from 1 to 5.

## Day 3: Slices and Maps

1.  **Favorite Colors**:
    *   Create a slice of strings containing your three favorite colors.
    *   Use `append` to add another color to the slice.
    *   Iterate over the slice using a `for` loop and print each color.
2.  **Simple Dictionary**:
    *   Create a map where keys are strings (e.g., "apple") and values are strings (e.g., "A fruit").
    *   Add 2-3 key-value pairs.
    *   Retrieve and print the definition of "apple".
    *   Use the two-value assignment to check if a key exists, e.g., `val, ok := myMap["banana"]`.

## Day 4: Structs and Pointers

1.  **User Profile**:
    *   Define a struct `User` with fields `Username` (string) and `IsActive` (bool).
    *   Create an instance of the `User` struct, populate its fields, and print it.
2.  **Age Updater**:
    *   Write a function `updateAge` that takes a pointer to an integer (representing a person's age).
    *   Inside the function, increment the age by 1.
    *   In `main`, declare an age variable, call `updateAge` with its address (`&age`), and then print the updated age.

## Day 5: Putting It Together

1.  **Simple Greeter Function**:
    *   Write a function that takes a `User` struct (from Day 4) as an argument.
    *   The function should print "Welcome, [Username]!" if the user `IsActive`, and "Goodbye, [Username]!" otherwise.
2.  **Review and Refactor**:
    *   Look back at the code you wrote this week.
    *   Run `gofmt` on all your files to ensure they are formatted correctly.
    *   Can you make any of the code cleaner or more readable?

Commit your code at the end of each day's practice to track your progress!
