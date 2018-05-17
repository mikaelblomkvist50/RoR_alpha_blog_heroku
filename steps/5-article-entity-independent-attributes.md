The **Article Entity** has 7 attributes. `id`, `title`, `description`, `slug`, `user_id`, `created_at` and `updated_at`. However some of these attributes rely on gems and other Entities therefore we only need to establish the independent attributes for the time being. Which are `id`, `title`, `description`, `created_at` and `updated_at`.

<pre><code>
$ <b>rails generate scaffold article title:string description:text</b>

$ <b>rake db:migrate</b>
== 20180406030357 CreateArticles: migrating ===================================
-- create_table(:articles)
   -> 0.0014s
== 20180406030357 CreateArticles: migrated (0.0015s) ==========================
$ <b>rm app/assets/stylesheets/scaffolds.scss</b>
</pre></code>
