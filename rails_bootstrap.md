# How To Add Bootstrap to a Rails 5 Project:

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







