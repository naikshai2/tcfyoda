# Create a Mock tCF Rails App

## New Rails App

In your terminal, go to where you want to store the Rails application
Alternatively, you can make a new directory. The ```mkdir``` command makes a new directory, and the ```cd``` command changes the directory.
<pre>
mkdir -p ~/code/
cd ~/code/
</pre>

Run this command to create a new Rails application with a specific version
<pre>
rails \_4.2.4_ new yodaforum
</pre>

Navigate into the new application and change the README to a markdown file. The ```mv``` command lets you rename files
<pre>
cd theCourseForum/
mv README.rdoc README.md
</pre>

## Configure Database

Open up the Gemfile, and replace the contents with the following code

<pre>
source 'https://rubygems.org' <br/>
gem 'rails', '4.2.4' <br/>
group :production do
  gem 'pg'
end <br/>
group :development do
  gem 'sqlite3'
end <br/>
# Use SCSS for stylesheets
gem 'sass-rails', '~> 5.0'
# Use Uglifier as compressor for JavaScript assets
gem 'uglifier', '>= 1.3.0'
# Use CoffeeScript for .coffee assets and views
gem 'coffee-rails', '~> 4.1.0'
# Use jquery as the JavaScript library
gem 'jquery-rails'
# Turbolinks makes following links in your web application faster. Read more: https://github.com/rails/turbolinks
gem 'turbolinks'
</pre>

Run bundle install

<pre>
bundle install
</pre>

Create the Database (sqlite)
<pre>
rake db:create
</pre>

Create a repository on Github for ```yodaforum```

Initialize the repository locally, add all the files, commit and push to Github
<pre>
$ git init
$ git add .
$ git commit -m 'First commit and README update'
$ git remote add origin git@github.com:username/repo_name.git
$ git push -u origin master
</pre>

## Static Pages

*This section is about MVC, making views, and routing*

MVC = Model View Controller. This is the software design pattern used to develop most web apps. Models are files which represent objects stored in the database. Views are html files which are displayed to the user. Controllers are files which handle HTTP requests.

### Generate the Controller and Views

<pre>
rails generate controller welcome index about
</pre>

Open up ```app/controllers/welcome_controller``` and look at the code. There are methods for the ```index``` and ```about``` actions.

Open up ```app/views/index.html.erb``` and ```app/views/about.html.erb```. These are the views for the ```index``` and ```about``` routes.

Start the server with ```rails s``` and navigate to ```localhost:3000/welcome/index``` and ```localhost:3000/welcome/about```

You should see placeholder text on the index and about pages.

### Routing in Rails

All of the routes are stored in the ```config/routes.rb``` file
This is what your routes should look like after generating the welcome controller with index and about actions:

<pre>
Rails.application.routes.draw do
  get "welcome/index"

  get "welcome/about"
  ...
end
</pre>

The HTTP ```GET``` command retrieves information with the url. ```welcome/index``` specifies that the welcome controller handles the index request.
If you comment out these two ```get``` lines in the routes file, there will be an error requesting ```localhost:3000/welcome/index``` and ```localhost:3000/welcome/about``` since those routes are no longer specified.

To view all of the routes in the applcition, run ```rake routes```
<pre>
$ rake routes
	Prefix Verb URI Pattern              Controller#Action
welcome_index GET /welcome/index(.:format) welcome#index
welcome_about GET /welcome/about(.:format) welcome#about
         root GET /                        welcome#index
</pre>

The output from ```rake routes``` is generated from the ```config/routes.rb``` file. As you can see, there are two ```GET``` routes specified from the ```welcome``` controller. The root route is also in the routes file.

Commit your changes and push to github.
<pre>
$ git add .
$ git commit -m "added static pages and messed with routes"
$ git push
</pre>


