# Ruby on Rails White Belt Projects

This is where you apply your new Ruby and Rails knowledge to build a complete web application from the ground up.

## Project: A Simple Blog

**Objective:** Build a basic blog where a user can create new posts, see a list of all posts, and view individual posts. This project touches on every core component of the MVC framework.

### Part 1: Planning and Setup

1.  **Generate the App**: Create a new Rails application named `simple_blog`.
    ```bash
    rails new simple_blog
    ```
2.  **Plan the Model**: We need a way to store blog posts. A `Post` will have a `title` (string) and `body` (text).

### Part 2: Creating the Posts

1.  **Generate the `Post` Model**: Use the `rails generate` command to create the model and the corresponding database migration file.
    ```bash
    rails generate model Post title:string body:text
    ```
2.  **Run the Migration**: Apply the changes to your database schema.
    ```bash
    rails db:migrate
    ```
3.  **Explore in the Console**:
    *   Open the Rails console: `rails console`.
    *   Create your first post: `Post.create(title: "My First Post", body: "This is the body of my very first post.")`
    *   Verify it was saved: `Post.all`

### Part 3: Displaying the Posts

1.  **Generate a `Posts` Controller**: We need a controller to handle requests related to posts. Let's create `index` (to list all posts) and `show` (to display one post) actions.
    ```bash
    rails generate controller Posts index show
    ```
2.  **Set up the Routes**: Open `config/routes.rb`. Rails may have added `get` routes for `index` and `show`. A better way is to use the `resources` method, which sets up all the standard RESTful routes for posts.
    ```ruby
    resources :posts
    root 'posts#index' # Set the blog index as the home page
    ```
3.  **List All Posts (Index Action)**:
    *   In `app/controllers/posts_controller.rb`, find the `index` method.
    *   Add this line to fetch all posts from the database: `@posts = Post.all`.
    *   In the corresponding view, `app/views/posts/index.html.erb`, write a loop to display each post's title.
    ```erb
    <h1>All Blog Posts</h1>
    <% @posts.each do |post| %>
      <h2><%= post.title %></h2>
    <% end %>
    ```
4.  **Show a Single Post (Show Action)**:
    *   In the `posts_controller.rb`, find the `show` method.
    *   Add this line to find the specific post the user is requesting: `@post = Post.find(params[:id])`.
    *   In the `index.html.erb` view, link each title to its show page: `<%= link_to post.title, post_path(post) %>`.
    *   In the `show.html.erb` view, display the post's title and body:
    ```erb
    <h1><%= @post.title %></h1>
    <p><%= @post.body %></p>
    ```

### Part 4: Creating New Posts

1.  **New and Create Actions**:
    *   The `resources :posts` line already created the routes for `new` and `create`.
    *   In `posts_controller.rb`, add the `new` and `create` actions.
    ```ruby
    def new
      @post = Post.new
    end

    def create
      @post = Post.new(post_params)
      if @post.save
        redirect_to @post # Redirect to the show page for the new post
      else
        render :new
      end
    end

    private

    def post_params
      params.require(:post).permit(:title, :body)
    end
    ```
    *   **Note**: The `post_params` method is a security feature called "Strong Parameters".

2.  **Create the Form (New View)**:
    *   In `app/views/posts/new.html.erb`, create a form that allows users to enter a title and body. Rails' `form_with` helper is perfect for this.
    ```erb
    <h1>New Blog Post</h1>
    <%= form_with model: @post do |form| %>
      <div>
        <%= form.label :title %><br>
        <%= form.text_field :title %>
      </div>
      <div>
        <%= form.label :body %><br>
        <%= form.text_area :body %>
      </div>
      <div>
        <%= form.submit %>
      </div>
    <% end %>
    ```
3.  **Add a "New Post" Link**: On the `index.html.erb` page, add a link to the new post form: `<%= link_to "New Post", new_post_path %>`.

Congratulations! You have now built a functional, database-driven web application with Ruby on Rails.
