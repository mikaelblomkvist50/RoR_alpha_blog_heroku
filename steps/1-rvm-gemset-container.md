1. $ rvm use **ruby_version_number**@**gemset_name** --create
2. $ gem install rails

   $ gem install rails --version=**rails_version_number**

   $ gem install rails --version=**rails_version_number** --no-ri --no-rdoc
3. $ rails new **project_name**
4. $ cd **project_name**
5. $ rvm --ruby-version use **ruby_version_number**@**gemset_name**
6. $ cat .ruby-version
7. $ cat .ruby-gemset

<pre><code>
$ <b>rvm use 2.4.1@BooksHerokuRoR --create</b>
ruby-2.4.1 - #gemset created /Users/yourname/.rvm/gems/ruby-2.4.1@BooksHerokuRoR
ruby-2.4.1 - #generating BooksHerokuRoR wrappers - please wait
Using /Users/yourname/.rvm/gems/ruby-2.4.1 with gemset BooksHerokuRoR

$ <b>gem install rails</b>
Fetching: concurrent-ruby-1.0.5.gem (100%)
Successfully installed concurrent-ruby-1.0.5
.
.
.
Fetching: rails-5.1.5.gem (100%)
Successfully installed rails-5.1.5
.
.
.
Parsing documentation for concurrent-ruby-1.0.5
Installing ri documentation for concurrent-ruby-1.0.5
.
.
.
Parsing documentation for rails-5.1.5
Installing ri documentation for rails-5.1.5
Done installing documentation for concurrent-ruby, i18n, thread_safe, tzinfo, activesupport, rack, rack-test, mini_portile2, n
okogiri, crass, loofah, rails-html-sanitizer, rails-dom-testing, builder, erubi, actionview, actionpack, activemodel, arel, ac
tiverecord, globalid, activejob, mini_mime, mail, actionmailer, nio4r, websocket-extensions, websocket-driver, actioncable, th
or, method_source, railties, bundler, sprockets, sprockets-rails, rails after 131 seconds
36 gems installed

$ <b>rails new books_heroku_RoR</b>

$ <b>cd books_heroku_RoR</b>

$ <b>rvm --ruby-version use 2.4.1@BooksHerokuRoR</b>
Using /Users/yourname/.rvm/gems/ruby-2.4.1 with gemset BooksHerokuRoR

$ <b>cat .ruby-version</b>
ruby-2.4.1

$ <b>cat .ruby-gemset</b>
BooksHerokuRoR
</code></pre>

Now if someone cloned your repository and `cd` into the repository it automatically creates the **gemset_name** for that user:
<pre><code>
<b>$ cd books_heroku_RoR</b>
ruby-2.4.1 - #gemset created /Users/yourname/.rvm/gems/ruby-2.4.1@BooksHerokuRoR
ruby-2.4.1 - #generating BooksHerokuRoR wrappers - please wai
</pre></code>

If you ever want to delete an existing `gemset`:
<pre><code>
<b>$ rvm gemset delete BooksHerokuRoR</b>
Are you SURE you wish to remove the entire gemset directory 'BooksHerokuRoR' (/Users/yourname/.rvm/gems/ruby-2.4.1@BooksHerokuRoR)?
(anything other than 'yes' will cancel) > yes
Removing gemset BooksHerokuRoR......
</pre></code>

If you ever want to use an existing `gemset`:
<pre><code>
<b>$ rvm gemset use BooksHerokuRoR</b>
Using ruby-2.4.1 with gemset BooksHerokuRoR
</pre></code>
