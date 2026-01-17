# Ruby on Rails - Green Belt Lessons

## Lesson 1: Performance Optimization

### Caching Strategies
```ruby
# Fragment caching
<% cache @product do %>
  <%= render @product %>
<% end %>

# Russian doll caching
<% cache ['product', @product] do %>
  <% cache ['reviews', @product.reviews] do %>
    <%= render @product.reviews %>
  <% end %>
<% end %>

# Low-level caching
Rails.cache.fetch("expensive_operation_#{id}", expires_in: 12.hours) do
  expensive_operation
end
```

---

## Lesson 2: Action Cable for Real-Time Features

### WebSocket Implementation
```ruby
# app/channels/chat_channel.rb
class ChatChannel < ApplicationCable::Channel
  def subscribed
    stream_from "chat_#{params[:room_id]}"
  end
  
  def receive(data)
    ActionCable.server.broadcast(
      "chat_#{params[:room_id]}",
      message: data['message']
    )
  end
end

# Broadcasting from anywhere
ChatChannel.broadcast_to(room, message: "Hello")
```

---

## Lesson 3: Service Objects Pattern

### Organizing Business Logic
```ruby
class UserRegistration
  def initialize(user_params)
    @user_params = user_params
  end
  
  def call
    ActiveRecord::Base.transaction do
      user = User.create!(@user_params)
      send_welcome_email(user)
      create_default_settings(user)
      user
    end
  rescue ActiveRecord::RecordInvalid => e
    Result.failure(e.record.errors)
  end
  
  private
  
  def send_welcome_email(user)
    WelcomeEmailJob.perform_later(user.id)
  end
  
  def create_default_settings(user)
    user.create_settings!(theme: 'light')
  end
end

# Usage
result = UserRegistration.new(params).call
```

---

## Lesson 4: Hotwire (Turbo + Stimulus)

### Modern Rails UX
```ruby
# Turbo Frame
<%= turbo_frame_tag "product_#{@product.id}" do %>
  <%= render @product %>
<% end %>

# Turbo Stream
# create.turbo_stream.erb
<%= turbo_stream.append "products" do %>
  <%= render @product %>
<% end %>

# Stimulus Controller
// app/javascript/controllers/dropdown_controller.js
import { Controller } from "@hotwire/stimulus"

export default class extends Controller {
  static targets = [ "menu" ]
  
  toggle() {
    this.menuTarget.classList.toggle("hidden")
  }
}
```

---

## Lesson 5: Deployment and DevOps

### CI/CD Pipeline
```yaml
# .github/workflows/ci.yml
name: CI
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: |
          bundle install
          rails db:setup
          rails test
      - name: Deploy
        if: github.ref == 'refs/heads/main'
        run: ./deploy.sh
```

---

## Lesson 6: Monitoring and Logging

### Production Observability
```ruby
# config/initializers/lograge.rb
Rails.application.configure do
  config.lograge.enabled = true
  config.lograge.custom_options = lambda do |event|
    {
      user_id: event.payload[:user_id],
      params: event.payload[:params].except(*Rails.application.config.filter_parameters)
    }
  end
end

# Monitoring with New Relic
newrelic.yml configuration
Custom instrumentation:
NewRelic::Agent.record_metric('Custom/MyMetric', value)
```

---

These advanced lessons prepare you for production Rails applications!
