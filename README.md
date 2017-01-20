# How To Create a New Rails 5 Project:

**Create a new Rails project**

*TERMINAL:* rails new name-of-your-app --database=postgresql

*TERMINAL:* cd name-of-your-app

**Open your project in Sublime**

*TERMINAL:* subl .

**Create your postgres database**

*TERMINAL:* rails db:create

**Run your Rails app**

*TERMINAL:* rails server

**Create a new terminal tab**
*TERMINAL:* (command + T)

**Create a controller**

*TERMINAL:* rails generate controller NameOfYourController (plural)
*Example:* rails generate controller Recipes

**Create a model**

*TERMINAL:* rails generate model ModelName attribute_1 attribute_2 attribute_3 ..etc... (singular model name)
*Example:* rails generate model Recipe title:string chef:string prep_time:integer

*TERMINAL:* rails db:migrate 

**Add items to the database**

*TERMINAL:* rails console

*CONSOLE:*
  x = ModelName.new({attribute_1: “some value”, attribute_2: “some value”})
  x.save
(repeat as desired)
  exit

**Add items to the database using the seeds.rb file (optional, but efficient)**

*FILE:* db/seeds.rb file

  x = ModelName.new({attribute_1: “some value”, attribute_2: “some value”})
  x.save

*TERMINAL:* rails db:seed


**Add Bootstrap to your project**

FILE: Gemfile
Add
  gem 'bootstrap-sass'
to the list of gems

EX: gem 'bootstrap-sass', '~> 3.3.6'

*TERMINAL:* bundle install

*FILE:* app/assets/stylesheets
  create a new file called _external.css.scss
Add these lines to that file:
  @import "bootstrap-sprockets";
  @import "bootstrap";

*FILE:* app/assets/javascripts/application.js
  add this line under the line that says //=require jquery: 
    //= require bootstrap-sprockets

**Restart the Rails server**
*TERMINAL:* (CONTROL + C)
*TERMINAL:* rails server







