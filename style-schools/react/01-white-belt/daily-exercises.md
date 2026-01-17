# React White Belt Daily Exercises

Practice these exercises daily to solidify your understanding of React fundamentals.

## Day 1: Understanding Components

1. **"Hello World" Component**:
    *   Create a new React project.
    *   Modify `App.js` (or a new component) to display `<h1>Hello, React!</h1>`.
    *   Experiment with rendering this component in `index.js`.
2. **Greeting Card**:
    *   Create a functional component called `GreetingCard`.
    *   Inside `GreetingCard`, render `<h2>Welcome to the Dojo!</h2>`.
    *   Render `GreetingCard` in `App.js`.

## Day 2: Props in Action

1. **Personalized Greeting**:
    *   Modify `GreetingCard` to accept a `name` prop.
    *   Display `<h2>Hello, {name}! Welcome to the Dojo!</h2>` using the prop.
    *   Render `GreetingCard` in `App.js` twice, passing different names (e.g., "Elder", "Student").
2. **Product Display**:
    *   Create a component `Product` that accepts `name`, `price`, and `description` as props.
    *   Render a few `Product` components with different data in `App.js`.

## Day 3: State and Event Handling

1. **Simple Counter**:
    *   Create a functional component `Counter`.
    *   Initialize state for a `count` with a value of 0.
    *   Display the current `count`.
    *   Add a button that, when clicked, increments the `count`.
    *   Add another button that decrements the `count`.
2. **Toggle Text**:
    *   Create a component `ToggleText`.
    *   Initialize state for `isVisible` (boolean).
    *   Display a paragraph of text conditionally based on `isVisible`.
    *   Add a button that toggles the `isVisible` state when clicked.

## Day 4: Conditional and List Rendering

1. **Login/Logout Button**:
    *   Create a component `AuthButton`.
    *   Use state `isLoggedIn` (boolean).
    *   Conditionally render "Login" or "Logout" button based on `isLoggedIn`.
    *   Make the button toggle `isLoggedIn` when clicked.
2. **Shopping List**:
    *   Create an array of items (e.g., `['Milk', 'Bread', 'Eggs']`).
    *   Create a component `ShoppingList`.
    *   Use the `map` function to render each item from the array as a `<li>` within an `<ul>`.

## Day 5: React Developer Tools & Review

1. **Inspect Components**:
    *   Open your browser's developer tools and navigate to the "Components" tab (for React Dev Tools).
    *   Inspect the props and state of the components you built in previous exercises.
    *   Try changing state/props directly in the Dev Tools to see the immediate effect.
2. **Refactor and Improve**:
    *   Take one of your previous exercises (e.g., the To-Do List from projects) and try to refactor it.
    *   Ensure components are clean, props are clearly defined, and state management is logical.

Remember to commit your code after each day's exercises!
