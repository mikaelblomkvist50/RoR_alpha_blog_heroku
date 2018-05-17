`app/controllers/articles_controller.rb`:
```ruby
Class ArticlesController < ApplicationController
  before_action :set_article, only: [:show, :edit, :update, :destroy]
.
.
.
  # POST /articles
  # POST /articles.json
  def create
    @article = Article.new(article_params)
    @article.user = User.first #hard code for time being

    respond_to do |format|
      if @article.save
        format.html { redirect_to @article, success: 'Article was successfully created.' }
        format.json { render :show, status: :created, location: @article }
      else
        format.html { render :new }
        format.json { render json: @article.errors, status: :unprocessable_entity }
      end
    end
  end
.
.
.
```

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
          <hr>
          <small>Created by: <%= article.user.username if article.user %>,
                             <%= time_ago_in_words(article.created_at) %> ago,
                            last updated: <%= time_ago_in_words(article.updated_at) %></small>
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
