`app/views/articles/show.html.erb`:
```html
<div class="card card-body bg-light">
  <h2 align="center"><%= @article.title %></h2>
  <hr>
  <h6><%= @article.description %></h6>
  <hr>

  <div align="center" class="article-actions">

      <%= link_to 'Edit this article', edit_article_path(@article), class: "btn btn-xs btn-warning" %>
      <%= link_to 'Delete this article', article_path(@article), method: :delete,
                                         data: { confirm: "Are you sure you want to delete the article?"},
                                         class: 'btn btn-xs btn-danger' %>
      <%= link_to 'View all articles', articles_path, class: "btn btn-xs btn-primary" %>
    </div>
</div>
```
