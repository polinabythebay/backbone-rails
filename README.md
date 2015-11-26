### Building a Rails application with Backbone.js, Coffeescript, and lodash.js

Set up Rails project

```
#create project specific Gemset and install Rails
rvm use ruby-2.2.3@backbone --ruby-version --create
gem install rails --version=4.1.6

#create new project in current directory. Exclude standard unit test packages.
rails new . -T

#create the database if not already created
rake db:create
```

Backbone and lodash

```
gem 'backbone-on-rails', '~> 1.1.0.0'
gem 'lodash-rails', '~> 2.2.1'
$ rails generate backbone:install
```





