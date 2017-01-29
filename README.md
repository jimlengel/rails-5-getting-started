How to make a new Rails app [with examples](new_crud.md)


  
# How To Create a New Rails 5 Project:

### Create a new Rails project

*in TERMINAL:* **rails new name-of-your-app --database=postgresql**

*in TERMINAL:* **cd name-of-your-app**

 

### Open your project in Sublime

*in TERMINAL:* **subl .**

 

### Create your postgres database

*in TERMINAL:* **rails db:create**

 

### Run your Rails app

*in TERMINAL:* **rails server**

 

#### Create a new in TERMINAL tab

*in TERMINAL:* **(command + T)**

 

#### Create a controller

*in TERMINAL:* rails generate controller NameOfYourController (plural)

*Example:* **rails generate controller Recipes**



#### Create a model

*in TERMINAL:* rails generate model ModelName attribute_1 attribute_2 attribute_3 ..etc... (singular model name)

*Example:* **rails generate model Recipe title:string chef:string prep_time:integer**

*in TERMINAL:* **rails db:migrate**



#### Add items to the database

*in TERMINAL:* **rails console**

*in CONSOLE:*

    x = ModelName.new({attribute_1: “some value”, attribute_2: “some value”})

    x.save

(repeat as desired)

    exit



#### Add items to the database using the seeds.rb file (optional, but efficient)

*in FILE:* db/seeds.rb file

    x = ModelName.new({attribute_1: “some value”, attribute_2: “some value”})

    x.save

*in TERMINAL:* **rails db:seed**



#### Add Bootstrap to your project

*in FILE:* Gemfile

Add

    gem 'bootstrap-sass'

to the list of gems

EX: gem 'bootstrap-sass', '~> 3.3.6'


*in TERMINAL:* **bundle install**

*in FOLDER:* app/assets/stylesheets

**create a new file called _external.css.scss**

**Add these lines to that file:**

    @import "bootstrap-sprockets";
    @import "bootstrap";

*in FILE:* app/assets/javascripts/application.js

add this line under the line that says //=require jquery

    //= require bootstrap-sprockets



#### Restart the Rails server

*in TERMINAL:* **(CONTROL + C)**

*in TERMINAL:* **rails server**







