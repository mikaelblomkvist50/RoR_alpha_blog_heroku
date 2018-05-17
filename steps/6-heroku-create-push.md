<pre><code>
$ <b>brew install heroku</b>

$ <b>which heroku</b>
/usr/local/bin/heroku

$ <b>heroku --version</b>
heroku-cli/6.15.26-5726b6f (darwin-x64) node-v9.5.0

$ <b>heroku login</b>

$ <b>heroku create</b>
Creating app... done, ⬢ dry-forest-22998
https://dry-forest-22998.herokuapp.com/ | https://git.heroku.com/dry-forest-22998.git

$ <b>heroku apps:rename books-heroku-ror</b>
Renaming dry-forest-22998 to books-heroku-ror... done
https://books-heroku-ror.herokuapp.com/ | https://git.heroku.com/books-heroku-ror.git
Git remote heroku updated
 ▸    Don't forget to update git remotes for all other local checkouts of the app.

$ <b>git push heroku master</b>

$ <b>heroku run rails db:migrate</b>

$ <b>heroku open</b>
</pre></code>
