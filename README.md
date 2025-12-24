# 🥋 Engineer Dojo: A Language-Agnostic Software Engineering Career Path

This repository contains a structured framework for progressing in a software engineering career, from Junior to Principal Engineer. It's designed to be language-agnostic, focusing on universal software engineering concepts.

## ⛩️ The Dojo Structure

The dojo is divided into three main sections:

-   **Core Belts**: These represent the universal software engineering knowledge that applies to any programming language. The belts range from White Belt (fundamentals) to Black Belt (Staff Engineer level).
-   **Dans**: These are post-Black Belt specializations for those on the Principal Engineer track.
-   **Style Schools**: These are optional, language-specific schools that teach you how to apply the core belt concepts in a specific technology like Go, React, or AWS.

## 🚀 How to Use the Dojo

### For Individual Learning

1.  Clone or fork this repository.
2.  Start at `core-belts/01-white-belt/`.
3.  Work your way through the `lessons.md`, `daily-exercises.md`, and choose a capstone project from `projects.md`.
4.  Use the `checklist.md` to self-assess your progress.
5.  Once you've completed a belt, move on to the next one.

### With an AI Assistant (like Gemini)

You can use an AI assistant to help you on your journey. For example, you can ask it to:

-   **Review your progress**: "I'm on the white belt and I've completed the CRUD API project. Can you review my code against the promotion requirements?"
-   **Suggest exercises**: "I have 20 minutes. What's a good orange-belt exercise?"
-   **Help you choose a project**: "Which capstone project should I pick for the yellow belt? I know Ruby and Go."

### For Teams

1.  Each engineer forks the repository.
2.  Each engineer tracks their progress in `examples/[username]/progress.md`.
3.  The team reviews capstone projects together.
4.  A senior engineer confirms when a promotion to the next belt is earned.

## ⚡ Quick Start

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/[username]/engineer-dojo.git
    cd engineer-dojo
    ```
2.  **Create your progress directory**:
    ```bash
    mkdir -p examples/[your-github]
    touch examples/[your-github]/progress.md
    ```
3.  **Start with the White Belt**:
    ```bash
    cd core-belts/01-white-belt
    ```
    -   Follow `lessons.md` and `daily-exercises.md`.
    -   Pick one project from `projects.md`.
4.  **Track your progress**:
    ```bash
    echo "## Week 1: White Belt" >> examples/[your-github]/progress.md
    git add .
    git commit -m "🥋 Week 1: Started White Belt"
    git push
    ```
5.  **Graduate to the next belt**:
    -   Complete all the items in the `checklist.md`.
    -   Get a code review from a peer or senior.
    -   Move on to `02-yellow-belt/`.
