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

### Discussion

If what you plan to build is something where the UI regularly changes how it displays but does not go to the server to get entire new pages then you probably need something like Backbone.js. An example of this is Gmail. It downloads everything once you first log in and then after that it does everything in the background. Backbone.js makes it easier to develop these kinds of rich single page applications. If you aren't trying to build a rich single page app and your backend server is doing all the heavy lifting, then you can probably just use Javascript/jQuery as icing on the cake.

An example of this is my Rails app where I made an urban dictionary for college students to login and vote and comment on entries. I spinkled a little bit of Ajax in there, but other than that my backend model is serving up static content by user request.

Backbone.js is a light framework that allows you to structure your Javascript code in MVC fashion. It's less than 1000 lines of code and very sensibly written. You can use it to add interactivity to your HTML pages! Once you start writing a lot of Javascript in your application, you start asking questions like:

- Where will I store my data?
- Where will I put my functions?
- How will I wire my functions together, so that they are called in a sensible way and don't turn to spaghetti?
- How can I make this code maintainable by different developers?

Backbone answers all of these questions:

- Models and Collections to help you represent data and collections of data.
- Views, to help you update your DOM when your data changes.
- An event system, so components can listen to each other. This keeps your components de-coupled, and prevents spaghettification.
- A minimal set of sensible conventions, so developers can work together on the same codebase.

### Pairing Rails and Backbone

Backbone originally started as a Javascript library in a Rails application, so it's history with Rails goes way back. Pairing both lends itself to an interesting conversation about what it means to create a RESTful web service.

Rails encourages users to create RESTful services by structuring its routing in terms of a set of resources accessed through uniform URI's (defined in routes.rb) through standard HTTP actions. This is important, because it makes this aspect of Rails **stateless**. This makes it really easy to turn a Javascript-light Rails app into an API. The Rails resources will essentially be the same, and instead of returning HTML it will return JSON.

#### Backbone, the stateful layer

Backbone is also based on RESTful services. Whenever you create, update or destroy a backbone.js model, you do so via the standard HTTP actions sent to URIs which assume a RESTful architecture. When you do this, you are essentially using Rails as an API. 

What happens when you do away with Rails' stateless HTML views? Previousing your users had a stateless interface for accessing RESTful resources. Now we have these access points:

- For humans: a rich, client-side interface provided by the backbone.js layer (stateful)
- For machines: a resource-oriented RESTful API provided by the rails layer (stateless)

Humans no longer have a stateless interface. A traditional Rails app has the following:

- HTML resources for humans (stateless)
- JSON/XML resources (API) for machines (stateless)

Other reasons why you should push towards a richer client-side application over server-side rendering:

- Persisting state in the DOM and relying on the server to update the UI means that your interface is only as fast as your network connection.
- Client-side MVC frameworks let you pull that logic into standalone JavaScript applications allowing you to separate out your concerns cleanly, re-render templates client-side and build responsive asynchronous interfaces.
- This is definitely a shift from the 'request/response model' I'm traditional used to in a Rails application. However, the upside is that we have to client side frameworks and tools to build desktop-like experiences for the web without our traditional 'click and wait' interaction.

#### Conclusion

I'm happy that I have started learning more Javascript and that I'm discovering the world of client-side rich applications. I don't think this is the end of Rails by any means-- 

- Rails still makes an excellent CRUD/REST API.
- Its asset pipeline makes it straightforward to serve up client side MVCs
- Has a good ORM, excellent libraries and community
- lacks Node's callback hell

I'm happy with relegating Rails to the API layer.

### Resources

- [Backbone on Rails book by thoughtbot](https://gumroad.com/l/backbone-js-on-rails)
- [Rails is just an API and that's okay](http://blog.alexmaccaw.com/rails-is-just-and-api-and-that-s-ok)
- [Rails and Backbone working together](http://stackoverflow.com/questions/11918586/rails-and-backbone-working-together)





