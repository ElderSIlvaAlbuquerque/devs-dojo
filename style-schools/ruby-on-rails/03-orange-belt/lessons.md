# Ruby on Rails - Orange Belt Lessons

## Lesson 1: Active Record Associations

### Core Concepts
```ruby
class User < ApplicationRecord
  has_many :posts, dependent: :destroy
  has_many :comments
  has_many :commented_posts, through: :comments, source: :post
end

class Post < ApplicationRecord
  belongs_to :user
  has_many :comments, dependent: :destroy
  has_many :commenters, through: :comments, source: :user
end

class Comment < ApplicationRecord
  belongs_to :user
  belongs_to :post
end
```

---

## Lesson 2: Authentication with Devise

### Setup
```ruby
# Gemfile
gem 'devise'

# Terminal
rails generate devise:install
rails generate devise User
rails db:migrate

# Routes
devise_for :users

# Controllers
class ApplicationController < ActionController::Base
  before_action :authenticate_user!
end
```

---

## Lesson 3: Authorization with Pundit

### Policy Pattern
```ruby
class PostPolicy < ApplicationPolicy
  def update?
    user == record.user || user.admin?
  end
  
  def destroy?
    user == record.user || user.admin?
  end
  
  class Scope < Scope
    def resolve
      if user.admin?
        scope.all
      else
        scope.where(user: user)
      end
    end
  end
end

# Controller
class PostsController < ApplicationController
  def update
    @post = Post.find(params[:id])
    authorize @post
    @post.update(post_params)
  end
end
```

---

## Lesson 4: Background Jobs

### Sidekiq Implementation
```ruby
class WelcomeEmailJob < ApplicationJob
  queue_as :default
  
  def perform(user_id)
    user = User.find(user_id)
    UserMailer.welcome_email(user).deliver_now
  end
end

# Trigger job
WelcomeEmailJob.perform_later(user.id)

# Schedule job
WelcomeEmailJob.set(wait: 1.hour).perform_later(user.id)
```

---

## Lesson 5: Testing with RSpec

### Model Tests
```ruby
RSpec.describe User, type: :model do
  it { should have_many(:posts) }
  it { should validate_presence_of(:email) }
  
  describe '#full_name' do
    it 'returns first and last name' do
      user = User.new(first_name: 'John', last_name: 'Doe')
      expect(user.full_name).to eq('John Doe')
    end
  end
end
```

### Request Specs
```ruby
RSpec.describe 'Posts API', type: :request do
  describe 'GET /posts' do
    it 'returns all posts' do
      create_list(:post, 3)
      get '/posts'
      expect(response).to have_http_status(:success)
      expect(JSON.parse(response.body).size).to eq(3)
    end
  end
end
```

---

These lessons cover essential Rails patterns for building web applications!
