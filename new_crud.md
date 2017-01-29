# Super Short Guide to creating a new Rails app

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

routes.rb
```
get ‘/‘ => 'books#index'
get ‘/books‘ => 'books#index'
```

books_controller.rb
```
def index
  @books = Book.all
end
```

index.html.erb
```   
<%= @books.each do |book| %>
  <p><%= book.name %></p>
<% end %>
```


# Routes

### master/config/routes.rb

```
Rails.application.routes.draw do
  get '/' => 'contacts#index'
  get '/contacts' => 'contacts#index'
  get '/contacts/new' => 'contacts#new'
  post '/contacts' => 'contacts#create'
  get '/contacts/:id' => 'contacts#show'
  get '/contacts/:id/edit' => 'contacts#edit'
  patch '/contacts/:id' => 'contacts#update'
  delete '/contacts/:id' => 'contacts#destroy'
end
```

# Controller

### app/controllers/contacts_controller.rb

```
class ContactsController < ApplicationController
  def index
      @contacts = Contact.all
    end

    def show
      @contact = Contact.find(params[:id])
    end

    def new
    end

    def create
      @contact = Contact.new(
                             first_name: params[:first_name], 
                             middle_name: params[:middle_name], 
                             last_name: params[:last_name], 
                             email: params[:email], 
                             phone_number: params[:phone_number],
                             bio: params[:bio]
                             )
      @contact.save
      flash[:success] = "Contact created."
      redirect_to "/contacts/#{@contact.id}"
    end

    def edit
      @contact = Contact.find(params[:id])
    end

    def update
      @contact = Contact.find(params[:id])
      @contact.assign_attributes(
                                 first_name: params[:first_name], 
                                 middle_name: params[:middle_name], 
                                 last_name: params[:last_name], 
                                 email: params[:email], 
                                 phone_number: params[:phone_number],
                                 bio: params[:bio]
                                 )
      @contact.save
      flash[:success] = "Contact updated."
      redirect_to "/contacts/#{@contact.id}"
    end

    def destroy
      @contact = Contact.find(params[:id])
      @contact.destroy
      flash[:success] = "Contact deleted."
      redirect_to "/"
    end
end
```

# Views 

### app/views/contacts/index.html.erb

```
<h1>Your Contacts</h1>
<% @contacts.each do |contact| %>
  <div>
    <h2><%= link_to "#{contact.first_name} #{contact.last_name}", "/contacts/#{contact.id}" %></h2>
    <h3>Email: <%= contact.email %></h3>
    <h3>Phone: <%= contact.phone_number %></h3>
  </div>
<% end %>
```

### app/views/contacts/show.html.erb

```
<h1><%= @contact.full_name %></h1>
<h4>Updated On: <%= @contact.friendly_updated_at %></h4>
<h2>Email: <%= @contact.email %></h2>
<h2>Phone: <%= @contact.phone_number %></h2>
<div>
  <h2>Bio:</h2>
  <p><%= @contact.bio %></p>
</div>
<%= link_to "Edit", "/contacts/#{@contact.id}/edit", class: "btn btn-info" %>
<%= link_to "Delete", "/contacts/#{@contact.id}", method: :delete, class: "btn btn-danger" %>
```

### app/views/contacts/new.html.erb

```
<h1>New Contact</h1>
<%= form_tag "/contacts", method: :post, class: "form-horizontal" do %>
  <div class="form-group">
    <%= label_tag :first_name, "First Name", class: "col-sm-2 control-label" %>
    <div class="col-sm-8">
      <%= text_field_tag :first_name, nil, class: "form-control" %>
    </div>
  </div>
  <div class="form-group">
    <%= label_tag :middle_name, "Middle Name", class: "col-sm-2 control-label" %>
    <div class="col-sm-8">
      <%= text_field_tag :middle_name, nil, class: "form-control" %>
    </div>
  </div>
  <div class="form-group">
    <%= label_tag :last_name, "Last Name", class: "col-sm-2 control-label" %>
    <div class="col-sm-8">
      <%= text_field_tag :last_name, nil, class: "form-control" %>
    </div>
  </div>
  <div class="form-group">
    <%= label_tag :email, "Email", class: "col-sm-2 control-label" %>
    <div class="col-sm-8">
      <%= text_field_tag :email, nil, class: "form-control" %>
    </div>
  </div>
  <div class="form-group">
    <%= label_tag :phone_number, "Phone Number", class: "col-sm-2 control-label" %>
    <div class="col-sm-8">
      <%= text_field_tag :phone_number, nil, class: "form-control" %>
    </div>
  </div>
  <div class="form-group">
    <%= label_tag :bio, "Bio", class: "col-sm-2 control-label" %>
    <div class="col-sm-8">
      <%= text_area_tag :bio, nil, class: "form-control" %>
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-offset-2 col-sm-8">
      <%= submit_tag "Create Contact", class: "btn btn-default" %>
    </div>
  </div>
<% end %>
```

### app/views/contacts/edit.html.erb
```
<h1>Edit Contact</h1>
<%= form_tag "/contacts/#{@contact.id}", method: :patch do %>
  <div>
    <%= label_tag :first_name %>
    <%= text_field_tag :first_name, @contact.first_name %>
  </div>
  <div>
    <%= label_tag :middle_name %>
    <%= text_field_tag :middle_name, @contact.middle_name %>
  </div>
  <div>
    <%= label_tag :last_name %>
    <%= text_field_tag :last_name, @contact.last_name %>
  </div>
  <div>
    <%= label_tag :email %>
    <%= text_field_tag :email, @contact.email %>
  </div>
  <div>
    <%= label_tag :phone_number %>
    <%= text_field_tag :phone_number, @contact.phone_number %>
  </div>
  <div>
    <%= label_tag :bio %>
    <%= text_area_tag :bio, @contact.bio %>
  </div>
  <div>
    <%= submit_tag "Update Contact" %>
  </div>
<% end %>
```

# Layouts

### app/views/layouts/application.html.erb

```
    <div class="container">  

    <% flash.each do |name, message| %>
     
      <div class="alert alert-<%= name %> alert-dismissible" role="alert">
      <button type="button" class="close" data-dismiss="alert"><span aria-hidden="true">&times;</span><span class="sr-only">Close</span></button>
      <%= message %>
    </div>
     
     <% end %>
    <%= yield %>

    </div>
```

# Models

### app/models/contact.rb

```
class Contact < ApplicationRecord
  def friendly_updated_at
    updated_at.strftime('%b %d, %Y')
  end

  def full_name
    "#{first_name} #{middle_name} #{last_name}".titleize
  end
end
```



