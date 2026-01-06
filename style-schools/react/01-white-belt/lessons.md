# React White Belt Lessons

Welcome to the React White Belt! This section will guide you through the foundational concepts of React.

## Lesson 1: Introduction to React and JSX

### What is React?
React is a JavaScript library for building user interfaces, primarily declarative UI. It allows developers to create large web applications that can change data without reloading the page. The main goal of React is to be fast, scalable, and simple.

* **Declarative vs. Imperative Programming**: Understand the difference and why React uses a declarative approach.
* **Single-Page Applications (SPAs)**: How React fits into building dynamic, single-page applications.

### Setting Up Your First React Project
We'll use `Create React App` (or Vite) for a quick setup, which provides a modern build setup with no configuration.

* `npx create-react-app my-app` (or `npm create vite@latest`)
* Understanding the basic project structure: `public/`, `src/`, `package.json`.

### JSX: JavaScript XML
JSX is a syntax extension for JavaScript. It's similar to a template language, but it comes with the full power of JavaScript.

* **Writing JSX**: How to embed HTML-like syntax directly in your JavaScript code.
* **Expressions in JSX**: Using curly braces `{}` to embed JavaScript expressions.
* **JSX Attributes**: Passing attributes to HTML elements and custom components.
* **Styling in JSX**: Basic inline styles and class names.

## Lesson 2: Components - The Building Blocks

### Functional Components
The most common way to write React components today. They are JavaScript functions that return JSX.

* **Defining a Functional Component**: `function MyComponent() { return <div>...</div>; }`
* **Rendering Components**: How components are rendered in the browser.
* **Component Composition**: Building complex UIs by combining smaller components.

### Understanding the Component Tree
Visualize how components are nested and form a tree structure, from the root `App` component down to the smallest elements.

## Lesson 3: Props - Passing Data

### What are Props?
Props (short for properties) are how you pass data from a parent component to a child component. They are read-only.

* **Passing Props**: How to send data from a parent component to a child component using attributes.
* **Receiving Props**: How a child component accesses the passed data.
* **Destructuring Props**: A common and clean way to extract data from the `props` object.
* **Default Props**: Providing fallback values for props if they are not explicitly passed.

## Lesson 4: State - Managing Dynamic Data

### What is State?
State is data that a component can manage and change over time. When state changes, the component re-renders.

* **`useState` Hook**: The fundamental hook for adding state to functional components.
    *   `const [value, setValue] = useState(initialValue);`
* **Updating State**: The correct way to update state using the setter function.
* **Immutability of State**: Why you should never directly modify state.
* **State vs. Props**: Understanding when to use state (internal, dynamic) vs. props (external, static from parent).

## Lesson 5: Event Handling

### Responding to User Interactions
How to handle events like clicks, form submissions, and input changes in React.

* **Synthetic Events**: React's cross-browser event system.
* **Event Handlers**: Attaching functions to events (e.g., `onClick`, `onChange`).
* **Passing Arguments to Event Handlers**: How to send extra data when an event occurs.

## Lesson 6: Conditional and List Rendering

### Conditional Rendering
Displaying different elements or components based on certain conditions.

* **`if` statements**: Using `if`/`else` inside component logic.
* **Logical `&&` operator**: Short-circuit rendering.
* **Ternary operator `? :`**: Inline conditional rendering.

### List Rendering
Displaying collections of data efficiently.

* **`map()` function**: The primary method for rendering lists of items.
* **`key` Prop**: Why the `key` prop is crucial for list performance and stability.
* **Rendering Lists of Components**: Creating a component for each item in a list.

## Lesson 7: Debugging with React Developer Tools

### Introduction to React Dev Tools
A browser extension that allows you to inspect React component hierarchies, props, state, and performance.

* **Installation**: How to install the extension for your browser.
* **Inspecting Components**: Navigating the component tree.
* **Viewing/Editing Props and State**: Debugging component data in real-time.
* **Profiling**: Basic understanding of how to use the profiler (optional for White Belt).

By the end of these lessons, you'll have a solid grasp of React's core principles and be ready to build simple, interactive applications!
