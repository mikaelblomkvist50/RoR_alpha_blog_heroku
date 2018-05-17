`Gemfile`:
```ruby
gem 'bcrypt', '~> 3.1', '>= 3.1.11'
```

<pre><code>
$ <b>bundle install --without production</b>

$ <b>rails generate migration add_password_digest_to_users password_digest:string</b>
Running via Spring preloader in process 10034
      invoke  active_record
      create    db/migrate/20180409083339_add_password_digest_to_users.rb


$ <b>rake db:migrate</b>
== 20180409083339 AddPasswordDigestToUsers: migrating =========================
-- add_column(:users, :password_digest, :string)
   -> 0.0013s
== 20180409083339 AddPasswordDigestToUsers: migrated (0.0014s) ================
</pre></code>

`app/models/user.rb`:
```ruby
class User < ApplicationRecord
  before_save {self.email = email.downcase}

  has_many :articles

  validates :username, presence: true,  uniqueness: {case_sensitive: false},
            length: {minimum: 3, maximum: 25}

  VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i
  validates :email, presence: true, length: {maximum: 105}, uniqueness: {case_sensitive: false},
            format: {with: VALID_EMAIL_REGEX}

  has_secure_password
end
```

<pre><code>
$ <b>rails console</b>
Running via Spring preloader in process 10577
Loading development environment (Rails 5.1.6)
2.4.1 :001 > user = User.new(username: "Julius", email: "julius@example.com", password_digest: nil)
 => <User id: nil, username: "Julius", email: "julius@example.com", created_at: nil, updated_at: nil, password_digest: nil>
2.4.1 :002 > user.password = "supersecret"
 => "supersecret"
2.4.1 :003 > user.save
   (0.1ms)  begin transaction
  User Exists (0.2ms)  SELECT  1 AS one FROM "users" WHERE LOWER("users"."username") = LOWER(?) LIMIT ?  [["username", "Julius"], ["LIMIT", 1]]
  User Exists (0.1ms)  SELECT  1 AS one FROM "users" WHERE LOWER("users"."email") = LOWER(?) LIMIT ?  [["email", "julius@example.com"], ["LIMIT", 1]]
  SQL (1.0ms)  INSERT INTO "users" ("username", "email", "created_at", "updated_at", "password_digest") VALUES (?, ?, ?, ?, ?)  [["username", "Julius"], ["email", "julius@example.com"], ["created_at", "2018-04-09 08:38:46.630879"], ["updated_at", "2018-04-09 08:38:46.630879"], ["password_digest", "$2a$10$fclsNZfNqOTcWEYUd8gxWud4yL5h6PDwVBTDZ0QshJ.MEql.GQRye"]]
   (1.7ms)  commit transaction
 => true
2.4.1 :004 > user.authenticate("is_this_your_password?")
 => false
2.4.1 :005 > user.authenticate("how_about_this_one?")
 => false
2.4.1 :006 > user.authenticate("supersecret")
 => <User id: 2, username: "Julius", email: "julius@example.com", created_at: "2018-04-09 08:38:46", updated_at: "2018-04-09 08:38:46", password_digest: "$2a$10$fclsNZfNqOTcWEYUd8gxWud4yL5h6PDwVBTDZ0QshJ....">
</pre></code>

`config/routes.rb`:
```ruby
Rails.application.routes.draw do
  resources :users, :except => [:new]
  resources :articles
  root 'welcome#index'

  get 'signup', to: 'users#new'

  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end
```

`app/views/users/_form.html.erb`:
```html
<%= form_with(model: user, local: true) do |form| %>
  <% if user.errors.any? %>
    <div class="alert alert-danger" role="alert">
      <h2><%= pluralize(user.errors.count, "error") %> prohibited this user from being saved:</h2>

      <ul>
        <% user.errors.full_messages.each do |message| %>
          <li><%= message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>

  <div class="form-group row">
    <%= form.label :username, class: "col-sm-2 col-form-label" %>
    <div class="col-sm-10">
      <%= form.text_field :username, id: :user_username, class: "form-control", placeholder: "Username" %>
    </div>
  </div>

  <div class="form-row">
    <div class="form-group col-sm-6">
      <%= form.label :email %>
      <%= form.email_field :email, id: :user_email, class: "form-control", placeholder: "name@example.com" %>
    </div>

    <div class="form-group col-sm-6">
      <%= form.label :password %>
      <%= form.password_field :password, class: "form-control" %>
    </div>
  </div>

  <div class="actions">
    <%= form.submit(@user.new_record? ? "Sign Up" : "Update account", class: "btn btn-primary")%>
  </div>
<% end %>
```

`app/controllers/users_controller.rb`:
```ruby
.
.
.
def create
    @user = User.new(user_params)

    respond_to do |format|
      if @user.save
        format.html { redirect_to articles_path, success: "Welcome to the alpha blog #{@user.username}, enjoy the articles! :)" }
        format.json { render :show, status: :created, location: @user }
      else
        format.html { render :new }
        format.json { render json: @user.errors, status: :unprocessable_entity }
      end
    end
  end

  # PATCH/PUT /users/1
  # PATCH/PUT /users/1.json
  def update
    respond_to do |format|
      if @user.update(user_params)
        format.html { redirect_to @user, success: 'User was successfully updated.' }
        format.json { render :show, status: :ok, location: @user }
      else
        format.html { render :edit }
        format.json { render json: @user.errors, status: :unprocessable_entity }
      end
    end
  end

  # DELETE /users/1
  # DELETE /users/1.json
  def destroy
    @user.destroy
    respond_to do |format|
      format.html { redirect_to users_url, danger: 'User was successfully destroyed.' }
      format.json { head :no_content }
    end
  end

  private
    # Use callbacks to share common setup or constraints between actions.
    def set_user
      @user = User.find(params[:id])
    end

    # Never trust parameters from the scary internet, only allow the white list through.
    def user_params
      params.require(:user).permit(:username, :email, :password)
    end
end
```
<pre><code>
$ <b>touch app/views/articles/_article.html.erb</b>
</pre></code>

`app/views/articles/_article.html.erb`:
```html
<h1 align="center">Listing all articles</h1>

<% obj.each do |article| %>
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
                            last updated: <%= time_ago_in_words(article.updated_at) %> ago</small>
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

`app/views/articles/index.html.erb`:
```html
<h1 align="center">Listing all articles</h1>

<%= render 'article', obj: @articles %>
```

`app/views/users/show.html.erb`:
```html
<h1 align="center">Welcome to <%= @user.username %>'s page</h1>
<div class="row">
  <div class="col-md-6 offset-md-3 text-center">
    <%= gravatar_for @user, size: 150 %>
  </div>
</div>

<h4 align="center"><%= @user.username %>'s articles</h4>

<%= render 'articles/article', obj: @user.articles %>

<div class="row">
  <div class="col-md-6 offset-md-3">.col-md-6 .offset-md-3</div>
</div>

<div class="row">
  <div class="col-md-6 offset-md-3 text-center">.col-md-6 .offset-md-3</div>
</div>
```
