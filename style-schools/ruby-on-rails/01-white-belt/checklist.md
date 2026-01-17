# Ruby on Rails White Belt Checklist

This checklist covers the fundamental Ruby and Rails concepts needed for your White Belt.

## Part 1: Ruby Fundamentals

*   [ ] What is Ruby? (Interpreted, dynamically typed, object-oriented).
*   [ ] Using `irb` (Interactive Ruby).
*   [ ] Variables and basic data types (`String`, `Integer`, `Float`, `Boolean`).
*   [ ] Printing output with `puts` and `print`.
*   [ ] Control Flow: `if`/`elsif`/`else`.
*   [ ] Collections:
    *   [ ] Arrays: creating, accessing, adding elements (`<<` or `.push`).
    *   [ ] Hashes: creating, accessing, adding key-value pairs.
*   [ ] Loops: `each`, `while`.
*   [ ] Methods: defining (`def`), calling, parameters, return values.
*   [ ] Basic Object-Oriented Programming (OOP):
    *   [ ] What is a class? What is an object (instance)?
    *   [ ] Defining a class with `class`.
    *   [ ] The `initialize` method.
    *   [ ] Instance variables (`@variable`).
    *   [ ] Creating an object with `.new`.

## Part 2: Rails Fundamentals

*   [ ] What is Ruby on Rails? (Web framework, MVC).
*   [ ] Installing Rails (`gem install rails`).
*   [ ] Creating a new Rails app (`rails new`).
*   [ ] Starting the Rails server (`rails server` or `bin/rails server`).
*   [ ] Understanding the **Model-View-Controller (MVC)** pattern:
    *   [ ] **Model**: Manages data and business logic.
    *   [ ] **View**: Displays data to the user (HTML templates).
    *   [ ] **Controller**: Handles user input and interacts with the model and view.
*   [ ] **Routing**:
    *   [ ] Editing `config/routes.rb`.
    *   [ ] Defining a route for the root path (`root 'controller#action'`).
    *   [ ] Using `resources` to create standard RESTful routes.
*   [ ] **Controllers**:
    *   [ ] Creating a controller with `rails generate controller`.
    *   [ ] Defining "actions" (public methods) in a controller.
*   [ ] **Views**:
    *   [ ] Understanding ERB (`.html.erb`) for embedding Ruby in HTML.
    *   [ ] How a controller action links to a view file.
    *   [ ] Passing data from a controller to a view using instance variables (`@variable`).
*   [ ] **Models & Databases**:
    *   [ ] Creating a model and migration with `rails generate model`.
    *   [ ] Understanding what a migration is.
    *   [ ] Running migrations with `rails db:migrate`.
    *   [ ] Interacting with the database via the Rails console (`rails console`).
    *   [ ] Basic Active Record methods: `.new`, `.create`, `.all`, `.find`.

## Projects

*   [ ] Build a simple "About Me" page with a dedicated route and controller action.
*   [ ] Create a basic blog application where you can create and display posts.

You've earned your White Belt when you can confidently check off these items!
