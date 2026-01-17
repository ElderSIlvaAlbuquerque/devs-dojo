# Ruby on Rails White Belt Daily Exercises

To learn Rails, you must first be comfortable with Ruby. The first few days focus exclusively on Ruby.

## Day 1: Ruby Variables & Methods

1.  **Greetings**:
    *   Open `irb` (Interactive Ruby).
    *   Create a variable `name` and assign your name to it as a string.
    *   Use `puts` to print "Hello, [Your Name]!".
2.  **Simple Method**:
    *   Define a method `say_hello(name)` that takes a name as an argument and prints the greeting.
    *   Call this method with your name.

## Day 2: Ruby Control Flow & Arrays

1.  **Number Checker**:
    *   Write a method `check_number(num)` that prints "Positive" if the number is greater than 0, "Negative" if less than 0, and "Zero" if it's 0.
2.  **Favorite Foods**:
    *   Create an array containing three of your favorite foods as strings.
    *   Use the `each` method to iterate over the array and print "I love to eat [food]!" for each one.
    *   Add a fourth food to the array using the `<<` operator and print the whole array.

## Day 3: Ruby Hashes & Looping

1.  **User Profile**:
    *   Create a hash representing a user. It should have keys `:name`, `:email`, and `:age`.
    *   Populate it with some sample data.
    *   Print the user's email address by accessing the hash value.
2.  **Iterate a Hash**:
    *   Using the hash from the previous exercise, use the `each` method to print each key-value pair in the format "Key: [key], Value: [value]".

## Day 4: Your First Rails Page

1.  **New Rails App**:
    *   Generate a new Rails application called `my_first_app`.
    *   `cd` into the new directory.
2.  **Generate a "Welcome" Controller**:
    *   Run `rails generate controller Welcome index`.
    *   This creates a `WelcomeController` with an `index` action, a view file, and a route.
3.  **Start the Server**:
    *   Run `rails server`.
    *   Visit `http://localhost:3000/welcome/index` in your browser. You should see the default page Rails created.
4.  **Customize the Page**:
    *   Open `app/views/welcome/index.html.erb` and change the content to "Hello, Rails!".
    *   Refresh your browser to see the change.

## Day 5: Creating a Root Route

1.  **Set the Root**:
    *   In your `my_first_app` project, open `config/routes.rb`.
    *   Add this line: `root 'welcome#index'`.
2.  **Test It**:
    *   Restart your Rails server if it's running.
    *   Now, visit `http://localhost:3000/`. You should see your "Hello, Rails!" page without having to navigate to `/welcome/index`.
3.  **Controller Data**:
    *   In `app/controllers/welcome_controller.rb`, add an instance variable to the `index` method: `@message = "I am learning Rails!"`.
    *   In your view (`app/views/welcome/index.html.erb`), use `<%= @message %>` to display the content of the variable.
    *   Refresh your browser and see the message appear.

Commit your code daily to build good habits!
