# Go White Belt Lessons

Welcome to the Go White Belt! These lessons provide the conceptual foundation you'll need to start writing Go programs.

## Lesson 1: Your First Go Program

### Introduction to Go
*   **What is Go?**: A compiled, statically-typed language with a focus on simplicity, concurrency, and performance.
*   **Environment Setup**: Installing the Go toolchain and configuring your workspace (`GOPATH`).

### "Hello, World!"
*   **Package `main`**: The entry point for an executable program.
*   **Function `main`**: The function that runs when you execute your program.
*   **`import "fmt"`**: Importing the standard "format" package for I/O operations.
*   **`fmt.Println()`**: The basic function for printing text to the console.
*   **`go run` and `go build`**: Understanding how to execute your code directly and how to compile it into a binary.

## Lesson 2: Variables, Types, and Constants

### Variables
*   **`var` keyword**: The standard way to declare a variable (e.g., `var age int`).
*   **Short Variable Declaration `:=`**: A concise way to declare and initialize a variable (e.g., `name := "Go"`). This is the most common method inside functions.
*   **Zero Values**: In Go, variables declared without an explicit initial value are given their *zero value* (e.g., 0 for integers, `false` for booleans, `""` for strings).

### Basic Data Types
*   **Integers**: `int`, `int8`, `int32`, `int64`, etc.
*   **Floating-Point**: `float32`, `float64`.
*   **Strings**: `string` (immutable sequences of bytes).
*   **Booleans**: `bool` (`true` or `false`).

### Constants
*   **`const` keyword**: Used to declare values that are fixed at compile time.

## Lesson 3: Control Flow

### `if / else`
*   Conditional logic in Go. A key feature is that `if` statements don't require parentheses around the condition.
*   `if` statements can also include a short initialization statement.

### `for` loop
*   Go has only one looping construct: the `for` loop.
*   **Basic `for` loop**: `for i := 0; i < 10; i++ { ... }` (C-style).
*   **`while` style loop**: `for condition { ... }`.
*   **Infinite loop**: `for { ... }`.
*   **`for...range`**: The idiomatic way to iterate over slices, arrays, maps, and strings.

## Lesson 4: Functions

### Defining Functions
*   **`func` keyword**: How to declare a function.
*   **Parameters and Return Types**: `func add(a int, b int) int { ... }`.
*   **Multiple Return Values**: A key feature of Go, often used to return a result and an error (e.g., `func doSomething() (int, error)`).

## Lesson 5: Pointers

### What is a Pointer?
*   A pointer is a variable that stores the memory address of another variable.
*   **`&` operator**: The "address of" operator. It gives you the memory address of a variable.
*   **`*` operator**: The "dereference" operator. It gives you the value that a pointer points to. Also used to declare a pointer type (e.g., `var p *int`).
*   **When to use pointers**: To allow a function to modify a variable's value directly, or to avoid copying large data structures.

## Lesson 6: Composite Types

### Arrays
*   Fixed-size collections of items of the same type. Rarely used directly in Go.

### Slices
*   The workhorse of Go. Slices are dynamically-sized, flexible views into the elements of an array.
*   **`make()`**: How to create a slice.
*   **`len()` and `cap()`**: Getting the length and capacity of a slice.
*   **`append()`**: Adding elements to a slice.

### Maps
*   Key-value stores, similar to dictionaries or hash maps in other languages.
*   **`make()`**: How to create a map.
*   **Adding, retrieving, and deleting items**.
*   **The "comma ok" idiom**: Checking for the existence of a key in a map.

### Structs
*   Used to create custom data types by grouping together fields.
*   **Defining a struct**: `type Person struct { Name string; Age int }`.
*   **Creating instances** and accessing fields using dot notation (`.`).

By grasping these core concepts, you'll be well-equipped to start building real applications with Go.
