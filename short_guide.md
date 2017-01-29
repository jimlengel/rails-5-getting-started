# Creating a new Rails app

## Super Short Guide

rails new crud_practice -database=postgresql

cd crud_practice

rake db:create

rails g controller books

rails g model Book name description

rake db:migrate

subl .

rails s


localhost:3030

rails c

Book.create(name: “Mighty Joe Young”, “monkeys do the darnedest things.”)

Book.create(name: “Johnson Brothers” “they were in a cabin.”)

Book.all


#### routes.rb
```
get ‘/‘ => 'books#index'
get ‘/books‘ => 'books#index'
```

#### books_controller.rb
```
def index
  @books = Book.all
end
```

#### index.html.erb
```   
<%= @books.each do |book| %>
  <p><%= book.name %></p>
<% end %>
```


