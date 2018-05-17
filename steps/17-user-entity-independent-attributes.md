The **User Entity** has 5 attributes. `id`, `username`, `email`, `created_at` and `updated_at`.

<pre><code>
$ <b>rails generate scaffold user username:string email:string</b>

$ <b>rake db:migrate</b>
== 20180409054503 CreateUsers: migrating ======================================
-- create_table(:users)
   -> 0.0026s
== 20180409054503 CreateUsers: migrated (0.0027s) =============================
</pre></code>
