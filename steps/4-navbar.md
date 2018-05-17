<pre><code>
$ <b>rails generate controller Welcome index</b>
</pre></code>

`config/routes.rb`:
```ruby
Rails.application.routes.draw do
  root 'welcome#index'
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end
```

<pre><code>
$ <b>touch app/views/layouts/navbar.html.erb</b>
</pre></code>

`app/views/layouts/application.html.erb`:
```
<!DOCTYPE html>
<html>
  <head>
    <title>BooksHerokuRor</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= render "layouts/navbar" %>
    <div class="container">
      <%= yield %>
    </div>
  </body>
</html>
```

Go to [Codepen](https://codepen.io/JuliusRobertOppenheimer/pen/JpwWRw?editors=1000) and grab the HTML for the Navbar that suits your needs. Then past that into `app/views/layouts/_navbar.html.erb`

Or just grab this one `app/views/layouts/_navbar.html.erb`:
```html
<nav class="navbar navbar-dark navbar-expand-md" style="background-color: #5f4987;">
  <%= link_to "AlphaBlog", root_path, class: "navbar-brand" %>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#mainNav3rd">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="mainNav3rd">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item"><a class="nav-link" href="#">Articles</a> </li>
      <!-- <li class="nav-item"><%= link_to "Articles", articles_path, class: "nav-link" </li> -->
      <li class="nav-item"><a class="nav-link" href="#">New Article</a> </li>
      <!-- <li class="nav-item"><%= link_to "New Article", new_article_path, class: "nav-link" </li> -->
      <li class="nav-item"><a class="nav-link" href="#">Users</a> </li>
      <!-- <li class="nav-item"><%= link_to "Users", users_path, class: "nav-link" </li> -->

      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">Categories</a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">All Categories</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Sports</a>
          <a class="dropdown-item" href="#">Programming</a>
          <a class="dropdown-item" href="#">Books</a>
          <a class="dropdown-item" href="#">Lifestyle</a>
          <a class="dropdown-item" href="#">Food</a>
          <a class="dropdown-item" href="#">Travel</a>
        </div>
      </li>
    </ul>

    <ul class="navbar-nav ml-auto">
      <li class="nav-item"><a class="nav-link" href="#">Sign Up</a></li>
      <!-- <li class="nav-item"><%= link_to "Sign Up", signup_path, class: "nav-link" </li> -->
      <li class="nav-item"><a class="nav-link" href="#">Login</a></li>
     </ul>
  </div>
</nav>
```
