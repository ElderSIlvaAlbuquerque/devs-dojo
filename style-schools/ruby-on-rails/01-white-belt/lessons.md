# Ruby on Rails White Belt Lessons

This curriculum starts with the basics of the Ruby language before moving on to the Rails framework.

## Part 1: Ruby Fundamentals

### Lesson 1: Introduction to Ruby
* **What is Ruby?**: An interpreted, high-level, dynamically typed, and purely object-oriented programming language.
* **`irb`**: Your best friend for experimenting. Learn to use Interactive Ruby from your terminal.
* **Variables & Data Types**: Strings, Integers, Floats, Booleans (`true`, `false`, `nil`).
* **Methods**: In Ruby, you call methods on objects. `puts` is a method. `def` is used to define new methods.

### Lesson 2: Collections - Arrays and Hashes
* **Arrays**: Ordered lists of items. Learn how to create them, add items (`<<`), and access items by their index.
* **Hashes**: Collections of key-value pairs. Learn how to create them and access values by their key. Ruby 1.9+ introduced a cleaner syntax for keys that are symbols: `{ name: "John", age: 30 }`.
* **Iteration**: The `.each` method is the most common way to loop over arrays and hashes.

### Lesson 3: Control Flow
* **Conditionals**: `if`, `elsif`, `else`, and `end`.
* **Truthiness**: In Ruby, only `false` and `nil` are "falsy". Everything else (including `0`, `""`, and empty arrays/hashes) is "truthy".

### Lesson 4: A Brief Intro to Object-Oriented Programming (OOP)
* **Everything is an Object**: The core principle of Ruby.
* **Classes and Instances**: A class is a blueprint (`String`). An instance is a specific object made from that blueprint (`"hello"`).
* **Defining a Class**: Using the `class` keyword.
* **`initialize` method**: The constructor, called when you create a new object with `.new`.
* **Instance Variables (`@`)**: Variables that belong to a specific instance of a class.

## Part 2: Introduction to Rails

### Lesson 5: What is Rails?
* **Web Framework**: A collection of libraries that provides a structure for developing web applications.
* **Convention over Configuration**: Rails makes assumptions so you don't have to configure every little detail.
* **MVC (Model-View-Controller)**: The core architectural pattern of Rails.
    *   **Model**: The "brain". Interacts with the database.
    *   **View**: The "face". What the user sees (HTML).
    *   **Controller**: The "traffic cop". Receives user requests and orchestrates the response.

### Lesson 6: Your First Rails Application
* **`rails new`**: The command to generate a new Rails application skeleton.
* **`bundle install`**: Rails uses Bundler to manage dependencies (gems).
* **`rails server`**: How to start the local development server.
* **The Request/Response Cycle**: A user's browser sends a request, it hits the Rails router, which sends it to a controller, which may talk to a model, and then renders a view to send back as the response.

### Lesson 7: Routing, Controllers, and Views
* **Routing (`config/routes.rb`)**: The router maps incoming URLs to specific controller actions. The `root` route is the homepage.
* **Controllers**: Ruby classes that inherit from `ApplicationController`. Public methods in a controller are called "actions".
* **Views**: ERB (`.html.erb`) files that live in `app/views`. They allow you to embed Ruby code inside your HTML to create dynamic content.
* **Instance Variables in MVC**: The controller passes data to the view using instance variables (`@my_variable`).

### Lesson 8: Models and Active Record
* **Models**: Ruby classes that inherit from `ApplicationRecord`. They represent the data in your application (e.g., a `User`, a `Post`, a `Product`).
* **Active Record**: The library (gem) that provides an interface between your models and the database. It allows you to create, read, update, and delete database records using Ruby objects.
* **Migrations**: Ruby files that describe changes to your database schema (like creating or modifying tables). You run them with `rails db:migrate`.
* **`rails console`**: An interactive shell for your application where you can interact with your models and data directly.

These lessons provide the groundwork for building your first real application in the projects section.
