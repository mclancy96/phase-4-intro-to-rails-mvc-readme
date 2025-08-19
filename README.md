# Rails MVC Architecture

Understanding how Rails organizes your code is key to building powerful web applications. At the heart of Rails is the Model-View-Controller (MVC) architecture, which helps you keep your code organized, maintainable, and easy to understand.

---

## What is MVC?

The MVC pattern separates your application into three main components, each with a specific responsibility:

- **Model:** Handles data, business logic, and rules (for example, interacting with database records).
- **View:** Handles what the user sees (HTML, templates, and layouts).
- **Controller:** Handles user input, interacts with models, and renders views.

This separation means you can work on the look of your app (views) without worrying about how data is stored (models), and vice versa. It also makes it easier to find and fix bugs, or add new features.

**Analogy:**
Think of MVC like a restaurant:
- The **Model** is the kitchen, where the food (data) is prepared.
- The **View** is the dining area, where customers see and enjoy their meal.
- The **Controller** is the waiter, taking orders from customers and bringing food from the kitchen to the table.

---

## Example: Generating a Controller

Let’s walk through a practical example. Suppose you want to create a welcome page for your app. You’ll need a controller to handle the request and a view to display the page.

To generate a controller called `Welcome` with an `index` action, run:

```sh
bin/rails generate controller Welcome index
```

This command does a lot for you automatically. It creates:
- `app/controllers/welcome_controller.rb` — the controller file
- `app/views/welcome/index.html.erb` — the view template for the index action
- (Optionally) updates `config/routes.rb` so you can access your new page

**Why is this helpful?**
Instead of creating each file by hand, Rails generators save you time and help you follow best practices.

---


## Setting Up a Route

For your new controller action to be accessible in the browser, you need to set up a route. Routes tell Rails which controller and action to use for a given URL.

In `config/routes.rb`, set the root route to the `index` action of the `WelcomeController`:

```ruby
root "welcome#index"
```

Now, when someone visits the root URL (`/`), Rails knows to send the request to the `index` action in your `WelcomeController`.

**More Route Examples:**

You can define routes for other pages or actions as your app grows. Here are some common examples:

```ruby
# Route for a static about page
get "/about", to: "pages#about"

# Route for a contact form
get "/contact", to: "contacts#new"
post "/contact", to: "contacts#create"

# Resourceful route for articles (generates all CRUD routes)
resources :articles

# Named route for a custom action
get "/dashboard", to: "users#dashboard", as: :dashboard
```

**What do these do?**
- `get "/about", to: "pages#about"` maps `/about` to the `about` action in `PagesController`.
- `resources :articles` creates all the standard routes for an `Article` resource (index, show, new, edit, create, update, destroy).
- `as: :dashboard` lets you use `dashboard_path` in your code for cleaner links.

**Tip:**
You can add as many routes as you need to support your app’s features. Check the [Rails Routing Guide](https://guides.rubyonrails.org/routing.html) for more details and advanced options.

---


## How Views Are Rendered

In Rails, most controller actions have a corresponding view file. By default, after a controller action runs, Rails will automatically look for a view template that matches the action’s name and the controller’s folder. For example, the `index` action in `WelcomeController` will try to render `app/views/welcome/index.html.erb` unless you tell it to do something different (like redirect or render a different template).

Let’s see what happens when you visit your site’s root URL:
1. The browser sends a request to `/`.
2. Rails uses the route you defined to find `WelcomeController#index`.
3. The `index` action runs any logic you’ve written.
4. Rails automatically looks for a view template at `app/views/welcome/index.html.erb` and renders it as HTML.

**Example Flow:**

```
Browser → Controller (Welcome#index) → Model (if needed) → View (index.html.erb) → Browser
```

If your controller action needs data from the database, it can ask the model for it and pass it to the view. If you want to render a different view or perform a redirect, you can do so explicitly in your controller action.

---

## Example Code

Here’s how the pieces fit together:

**Controller:**
```ruby
class WelcomeController < ApplicationController
  def index
    # Any logic here, e.g. @greeting = "Hello, Rails!"
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
<!-- You can use Ruby code here, e.g. <%= @greeting %> -->
```

**Try it out:**
Add a variable in your controller:

```ruby
def index
  @greeting = "Hello, Rails!"
end
```

Then display it in your view:

```erb
<h1><%= @greeting %></h1>
```

This is how data flows from your controller to your view!

---

## Wrapping Up

The MVC pattern is the backbone of every Rails application. As you build more features, you’ll see how controllers, models, and views work together to handle everything from simple pages to complex data-driven apps. Don’t hesitate to experiment—try adding new actions, routes, and views to see how they connect!
