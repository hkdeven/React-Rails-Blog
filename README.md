# React on Rails Basic Tutorial

This walkthrough will help you setup your own, new Rails app with **React on Rails**, demonstrating Rails + React + Redux + Server Rendering.

![example](https://cloud.githubusercontent.com/assets/371302/17368567/111cc722-596b-11e6-9b72-ac5967a60e42.gif)

By the time you read this, the latest may have changed. Be sure to check the versions here:

* https://rubygems.org/gems/react_on_rails
* https://www.npmjs.com/package/react-on-rails

##Setting up the environment

Trying out **React on Rails** is super easy, so long as you have the basic prerequisites. This includes the basics for Rails 4.x and node version 5+. Ensure that you have Node, Rails, and Ruby installed and updated before proceeding.

Then we need to create a fresh Rails application as following:

```
cd <basic directory where you want to create your new Rails app>

rails new test-react-on-rails       # any name you like

cd test-react-on-rails
```

Add **React On Rails** gem to your Gemfile (`vim Gemfile` or `nano Gemfile` or in IDE):

```
gem 'react_on_rails', '~>6'         # use latest gem version > 6
```

Swap out sqlite for postgres.  In your gem file delete the line with `sqlite` and replace it with:

```ruby
   gem 'pg'
```

Replace your `database.yml` file with this (assuming your app name is "ror").

```yml
default: &default
  adapter: postgresql
  username:
  password:
  host: localhost

development:
  <<: *default
  database: ror_development

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  <<: *default
  database: ror_test

production:
  <<: *default
  database: ror_production
```

Then you need to setup postgres before you can run locally:

```
bundle
rake db:setup
rake db:migrate
```

I'd recommend adding this line to the top of your `routes.rb`. That way, your root page will go to the Hello World page for React On Rails.

```ruby
root "hello_world#index"
```

put everything under git repository (or `rails generate` will not work properly)

```
# Here are git commands to make a new git repo and commit everything
git init
git add -A
git commit -m "Initial commit"
```

update dependencies and generate empty app via `react_on_rails:install`. If you haven't done first git commit it will generate error and you just need to commit.

```
bundle
rails generate react_on_rails:install
bundle && npm install
```

and then run server with

```
foreman start -f Procfile.dev
```

Visit http://localhost:3000/hello_world and see your **React On Rails** app running!


Then after all changes are done don't forget to commit them with git and finally you can push your app to Heroku!

```
git add -A
git commit -m "Latest changes"
git push heroku master
```
