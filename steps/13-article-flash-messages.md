`app/controllers/application_controller.rb`:
```ruby
class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception
  add_flash_types :success, :warning, :danger
end
```

`app/views/application.html.erb`:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>AlphaBlogHerokuRor</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= render "layouts/navbar" %>
    <div class="container">
      <% flash.each do |name, message| %>
        <div class="alert alert-<%= "#{name}" %>">
          <a href="#" class="close" data-dismiss="alert">&#215;</a>
          <%= message %>
        </div>
      <% end %>
      <%= yield %>
    </div>
    <%= render "layouts/footer" %>
  </body>
</html>
```

`app/controllers/articles_controller.rb`
```ruby
class ArticlesController < ApplicationController
  before_action :set_article, only: [:show, :edit, :update, :destroy]

  # GET /articles
  # GET /articles.json
  def index
    @articles = Article.all
  end

  # GET /articles/1
  # GET /articles/1.json
  def show
  end

  # GET /articles/new
  def new
    @article = Article.new
  end

  # GET /articles/1/edit
  def edit
  end

  # POST /articles
  # POST /articles.json
  def create
    @article = Article.new(article_params)

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

  # PATCH/PUT /articles/1
  # PATCH/PUT /articles/1.json
  def update
    respond_to do |format|
      if @article.update(article_params)
        format.html { redirect_to @article, success: 'Article was successfully updated.' }
        format.json { render :show, status: :ok, location: @article }
      else
        format.html { render :edit }
        format.json { render json: @article.errors, status: :unprocessable_entity }
      end
    end
  end

  # DELETE /articles/1
  # DELETE /articles/1.json
  def destroy
    @article.destroy
    respond_to do |format|
      format.html { redirect_to articles_url, danger: 'Article was successfully destroyed.' }
      format.json { head :no_content }
    end
  end

  private
    # Use callbacks to share common setup or constraints between actions.
    def set_article
      @article = Article.friendly.find(params[:id])
    end

    # Never trust parameters from the scary internet, only allow the white list through.
    def article_params
      params.require(:article).permit(:title, :description)
    end
end
```

`app/views/articles/_form.html.erb`:
```html
<%= form_with(model: article, local: true) do |form| %>
  <% if article.errors.any? %>
    <div class="alert alert-danger" role="alert">
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
