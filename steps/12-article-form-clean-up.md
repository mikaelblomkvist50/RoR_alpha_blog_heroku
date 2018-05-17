`app/views/articles/_form.html.erb`:
```html
<%= form_with(model: article, local: true) do |form| %>
  <% if article.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(article.errors.count, "error") %> prohibited this article from being saved:</h2>

      <ul>
      <% article.errors.full_messages.each do |message| %>
        <li><%= message %></li>
      <% end %>
      </ul>
    </div>
  <% end %>

  <div class="form-group align-self-center">
    <%= form.label :title %>
    <%= form.text_field :title, id: :article_title, class: "form-control" %>
  </div>

  <div class="form-group align-self-center">
    <%= form.label :description %>
    <%= form.text_area :description, id: :article_description, :rows => 8, class: "form-control", placeholder: "Description Text...." %>
  </div>

  <div class="actions">
    <%= form.submit class: "btn btn-primary"%>
  </div>
<% end %>
```

<pre><code>
$ <b>touch app/assets/stylesheets/article_form.scss</b>
</pre></code>

`app/assets/stylesheets/article_form.scss`:
```css
#article_description {
  resize: none;
}
```

`app/assets/stylesheets/application.scss`:
```css
// Custom bootstrap variables must be set or imported *before* bootstrap.
@import "bootstrap";
@import 'article_form'
```
