# React White Belt Projects

These projects are designed to help you apply the fundamental concepts learned in the React White Belt lessons and daily exercises. Each project builds on the skills acquired, allowing you to create small, functional React applications.

## Project 1: Simple Static Portfolio Page

**Objective:** Create a basic, multi-component static portfolio page to showcase your understanding of JSX, components, and props.

**Requirements:**

1.  **App Component:** Your main `App.js` component should orchestrate the layout.
2.  **Header Component:**
    *   Displays your name (passed as a prop).
    *   Displays a simple navigation (e.g., "Home", "About", "Projects" - these don't need to be functional links, just text).
3.  **About Section Component:**
    *   Displays a short paragraph about yourself (e.g., "Hi, I'm [Your Name], an aspiring React developer.").
    *   Could include a simple image (optional, use a placeholder URL if needed).
4.  **Project Card Component:**
    *   Accepts `title`, `description`, and `link` (optional) as props.
    *   Displays this information in a structured way.
5.  **Projects Section Component:**
    *   Uses the `ProjectCard` component multiple times to display at least 3-4 dummy projects.
    *   Use an array of project data and `map` to render them.
6.  **Footer Component:**
    *   Displays a simple copyright notice.

**Concepts Reinforced:**
*   Functional Components
*   JSX
*   Props
*   Component Composition
*   List Rendering (for projects)

## Project 2: Interactive To-Do List

**Objective:** Build a functional To-Do List application that allows users to add new tasks, mark tasks as complete, and delete tasks. This project will heavily utilize state and event handling.

**Requirements:**

1.  **Task Input:**
    *   An `input` field where users can type a new task.
    *   A "Add Task" button.
2.  **Task List Display:**
    *   Display a list of tasks. Each task should show its text.
3.  **Mark as Complete:**
    *   Next to each task, there should be a way to mark it as complete (e.g., a checkbox or a "Complete" button).
    *   Completed tasks should visually differentiate themselves (e.g., strike-through text, different color).
4.  **Delete Task:**
    *   Next to each task, a "Delete" button that removes the task from the list.
5.  **State Management:**
    *   Manage the list of tasks using React's `useState` hook. Each task should be an object with `id`, `text`, and `completed` properties.
6.  **Event Handling:**
    *   Handle form submission for adding tasks.
    *   Handle click events for completing and deleting tasks.

**Concepts Reinforced:**
*   State (`useState`)
*   Event Handling
*   Conditional Rendering (for completed tasks)
*   List Rendering and `key` prop
*   Managing arrays in state
*   Form Handling (basic)

## Project 3: Simple Counter with Features

**Objective:** Enhance a basic counter application with more features to deepen your understanding of state, event handling, and conditional rendering.

**Requirements:**

1.  **Display Counter Value:** Show the current count prominently.
2.  **Increment Button:** Increases the count by 1.
3.  **Decrement Button:** Decreases the count by 1.
4.  **Reset Button:** Sets the count back to 0.
5.  **Step Input (Optional but Recommended):**
    *   An input field where the user can define a "step" value (e.g., 1, 5, 10).
    *   When incrementing/decrementing, the count should change by this step value instead of always by 1.
6.  **Conditional Styling/Text:**
    *   If the count is 0, display a message like "Count is zero!" in a different color.
    *   If the count is negative, display the number in red.
    *   If the count is positive, display the number in green.
7.  **Disable Decrement at Zero (Optional):**
    *   Disable the decrement button if the count is already 0 to prevent negative numbers (unless you implement negative number styling).

**Concepts Reinforced:**
*   State (`useState`)
*   Event Handling
*   Conditional Rendering and Styling
*   Input Field Handling

These projects will give you practical experience and confidence to move forward in your React journey. Good luck!
