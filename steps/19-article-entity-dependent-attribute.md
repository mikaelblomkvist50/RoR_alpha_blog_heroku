The **Article Entity** has 1 dependent attribute which is `user_id`.

<pre><code>
$ <b>rails generate migration add_user_id_to_articles user_id:integer</b>
Running via Spring preloader in process 7334
      invoke  active_record
      create    db/migrate/20180409060247_add_user_id_to_articles.rb

$ <b>rake db:migrate</b>
== 20180409060247 AddUserIdToArticles: migrating ==============================
-- add_column(:articles, :user_id, :integer)
   -> 0.0018s
== 20180409060247 AddUserIdToArticles: migrated (0.0019s) =====================
</pre></code>

`app.models/article.rb`:
```ruby
class Article < ApplicationRecord
  belongs_to :user

  validates :user_id, presence: true
  validates :title, presence: true, length: { minimum: 3, maximum: 50}
  validates :description, presence: true, length: { minimum: 10, maximum: 300}

  extend FriendlyId
  friendly_id :title, use: [:slugged, :history]

  def should_generate_new_friendly_id?
    slug.blank? || title_changed?
  end
end
```

`app.models/user.rb`:
```ruby
class User < ApplicationRecord
  before_save {self.email = email.downcase}

  has_many :articles

  validates :username, presence: true,  uniqueness: {case_sensitive: false},
            length: {minimum: 3, maximum: 25}

  VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i
  validates :email, presence: true, length: {maximum: 105}, uniqueness: {case_sensitive: false},
            format: {with: VALID_EMAIL_REGEX}
end
```
