# Getting Started with Ruby on Rails

1.  **Install Ruby**: Follow the instructions on the [official Ruby website](https://www.ruby-lang.org/en/documentation/installation/) to install Ruby.
2.  **Install Rails**: Run `gem install rails`.
3.  **Create a new Rails app**: Run `rails new myapp`.

## Code Style and Formatting

The Ruby community values clean, readable, and consistent code. The most widely adopted tool for maintaining this standard is **RuboCop**.

*   **`RuboCop`**: A powerful static code analyzer (linter) and formatter for Ruby. It enforces the guidelines outlined in the community-driven [Ruby Style Guide](https://github.com/rubocop/ruby-style-guide).
    *   **Installation**: Add `gem 'rubocop', require: false` to your Gemfile.
    *   **Usage**: Run `bundle exec rubocop` in your project's root to check for offenses. Use `bundle exec rubocop -A` to automatically correct many of the detected issues.
    *   **Configuration**: You can customize its behavior by creating a `.rubocop.yml` file in your project to enable/disable specific rules (known as "cops").

Integrating RuboCop into your workflow is a core practice for any serious Ruby/Rails developer.
