`article.rb`:
```ruby
class Article < ApplicationRecord
  validates :title, presence: true, length: { minimum: 3, maximum: 50}
  validates :description, presence: true, length: { minimum: 10, maximum: 300}

  extend FriendlyId
  friendly_id :title, use: [:slugged, :history]

  def should_generate_new_friendly_id?
    slug.blank? || title_changed?
  end
end
```
