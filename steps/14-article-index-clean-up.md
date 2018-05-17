`app/views/articles/index.html.erb`:
```html
<h1 align="center">Listing all articles</h1>

<% @articles.each do |article| %>
  <div class="row articles">
    <div class="col-lg-10 offset-lg-1">
      <div class="card card-body bg-light">

        <div align="center" class="article-title">
          <%= link_to article.title, article_path(article) %>
        </div>

        <div class="article-body">
          <%= truncate(article.description, length: 100) %>
        </div>

        <div align="center" class="article-actions">
          <hr>
          <%= link_to 'Edit this article', edit_article_path(article), class: "btn btn-xs btn-warning" %>
          <%= link_to 'Delete this article', article_path(article), method: :delete,
                                             data: { confirm: "Are you sure you want to delete the article?"},
                                             class: 'btn btn-xs btn-danger' %>
        </div>

      </div>
    </div>
  </div>
<% end %>
```

`app/assets/stylesheets/application.scss`:
```css
// Custom bootstrap variables must be set or imported *before* bootstrap.
@import "bootstrap";
@import 'footer';
@import 'article_form';

nav {
  margin-bottom: 30px;
}

ul {
  list-style: none;
  padding: 0px;
}


.articles {
  margin-bottom: 20px;
}

.article-title {
  font-weight: bold;
  font-size: 1.5em;
}

@include media-breakpoint-only(xs) {
  .btn-block-xs-only {
    margin-bottom: 5px;
    display: block;
    width: 100%;
  }
}
```
