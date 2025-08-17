# Rails MVC Architecture

Ruby on Rails is built around the Model-View-Controller (MVC) architecture, which separates your application into three main components:

- **Model:** Handles data, business logic, and rules (e.g., database records).
- **View:** Handles what the user sees (HTML, templates).
- **Controller:** Handles user input, interacts with models, and renders views.

## Example: Generating a Controller

To generate a controller called `Welcome` with an `index` action, run:

```sh
bin/rails generate controller Welcome index
```

This creates:
- `app/controllers/welcome_controller.rb`
- `app/views/welcome/index.html.erb`
- A route in `config/routes.rb` (if you add it)

## Setting Up a Route

In `config/routes.rb`, set the root route to the `index` action of the `WelcomeController`:

```ruby
root "welcome#index"
```

## How Views Are Rendered

When you visit the root URL (`/`), Rails will:
1. Route the request to `WelcomeController#index`
2. Run the `index` action
3. Render the view at `app/views/welcome/index.html.erb`

## Example Code

**Controller:**
```ruby
class WelcomeController < ApplicationController
  def index
    # Any logic here
  end
end
```

**Route:**
```ruby
# config/routes.rb
root "welcome#index"
```

**View:**
```erb
<!-- app/views/welcome/index.html.erb -->
<h1>Welcome to Rails!</h1>
```

---

This is the basic flow of MVC in Rails!
