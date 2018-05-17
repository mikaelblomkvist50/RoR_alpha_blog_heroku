Make sure the file has .scss extension (or .sass for Sass syntax). If you have just generated a new Rails app, it may come with a .css file instead. If this file exists, it will be served instead of Sass, so rename it:
<pre><code>
$ <b>mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss</b>
</pre></code>

Then, remove all the *= require and *= require_tree statements from the Sass file. Instead, use @import to import Sass files.

Import Bootstrap styles in `app/assets/stylesheets/application.scss`:
```
// Custom bootstrap variables must be set or imported *before* bootstrap.
@import "bootstrap";
```
The available variables can be found [here](assets/stylesheets/bootstrap/_variables.scss).

**Bootstrap** JavaScript depends on **jQuery**. If you're using **Rails 5.1+**, add the `jquery-rails gem` to your Gemfile. **Bootstrap** tooltips and popovers depend on **popper.js** for positioning. The `bootstrap gem` already depends on the `popper_js gem` which is greate beacue it saves us from placing it in the Gemfile our selves.

```ruby
gem 'jquery-rails', '~> 4.3', '>= 4.3.1'
gem 'bootstrap', '~> 4.0'
```

The jquery and jquery-ujs files will be added to the asset pipeline and available for you to use. If they're not already in app/assets/javascripts/application.js by default, add these lines:
```js
//= require jquery3
//= require jquery_ujs
```

If you are running Rails 5.1 and up, and if you have included //= require rails-ujs, then jquery_ujs is not needed anymore. You can just add:
```js
//= require jquery3
//= require rails-ujs
```

Add Bootstrap dependencies and Bootstrap to your application.js:
```js
//= require jquery3
//= require popper
//= require bootstrap-sprockets
```

So ithe app/assets/javascripts/application.js becomes:
```js
// This is a manifest file that'll be compiled into application.js, which will include all the files
// listed below.
//
// Any JavaScript/Coffee file within this directory, lib/assets/javascripts, or any plugin's
// vendor/assets/javascripts directory can be referenced here using a relative path.
//
// It's not advisable to add code directly here, but if you do, it'll appear at the bottom of the
// compiled file. JavaScript code in this file should be added after the last require_* statement.
//
// Read Sprockets README (https://github.com/rails/sprockets#sprockets-directives) for details
// about supported directives.
//
//= require jquery3
//= require rails-ujs
//= require popper
//= require bootstrap-sprockets
//= require turbolinks
//= require_tree .
```

<pre><code>
$ <b> bundle install --without production</b>
</pre></code>
