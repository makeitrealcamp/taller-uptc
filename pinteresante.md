# Pinteresante

A continuación encontrarás los requisitos y listados de código para construir un clon de Pinterest en Ruby on Rails.

## Requerimientos

* Un editor de texto, nuestra recomendación es [Sublime Text](http://www.sublimetext.com/)
* Git, Ruby y Ruby on Rails. Si estás en Mac o Linux sigue las instrucciones en http://installrails.com/. Para Windows sigue las instrucciones en:
  * Git: https://makeitreal.wistia.com/medias/9jjnpri7lf
  * Ruby: https://makeitreal.wistia.com/medias/b85w0goonx

Opcional:

* Crea una cuenta en [Github](https://github.com/).
* Crea una cuenta en [Heroku](http://heroku.com/).
* Descarga el [Heroku Toolbelt](https://toolbelt.heroku.com/).

## Listados

### Crear el proyecto

**Listado 1**.

```
$ rails new pinteresante
```

**Listado 2**.

```
$ git init
$ git add .
$ git commit -m 'Versión inicial'
```

### Configurar Bootstrap y Devise

Bootstrap: https://github.com/twbs/bootstrap-sass<br>
Devise: https://github.com/plataformatec/devise

**Listado 3**. En el archivo `Gemfile`.

```
gem 'bootstrap-sass', '~> 3.3.5'
```

**Listado 4**. En el archivo `app/assets/stylesheets/application.scss`

```
@import "bootstrap-sprockets";
@import "bootstrap";
```

**Listado 5**. En el archivo `app/assets/javascripts/application.js`

```
//= require bootstrap-sprockets
```

**Listado 6**.

```
$ bundle install
$ git add .
$ git commit -m 'Configura Bootstrap'
```

**Listado 7**. En el archivo `Gemfile`.

```
gem 'devise'
```

**Listado 8**.

```
$ bundle install
```

**Listado 9**.

```
$ rails generate devise:install
```

**Listado 10**.

```
$ rails generate devise User
$ rake db:migrate
$ rails generate devise:views
```

**Listado 11**. En `app/views/layouts/application.html.erb`

```
<nav class="navbar navbar-default">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">Pinteresante</a>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav navbar-right">
        <% if signed_in? %>
          <li><%= link_to "Salir", destroy_user_session_path, method: :delete %></li>
        <% else %>
          <li><%= link_to "Registrarse", new_user_registration_path %></li>
          <li><%= link_to "Ingresar", new_user_session_path %></li>
        <% end %>
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
```

**Listado 12**.

```
$ git add .
$ git commit -m 'Configura Devise'
```

### Implementar la funcionalidad

**Listado 13**.

```
$ rails g resource Pin user:references title image_url
$ rake db:migrate
```

**Listado 14**. En `app/controllers/pins_controller.rb`

```
def index
  @pins = Pin.all
end
```

**Listado 15**. En `app/views/pins/index.html.erb`

```
<div id="pins">
<% @pins.each do |pin| %>
  <div class="pin panel panel-default">
    <div class="panel-body">
      <img src="<%= pin.image_url %>" alt="<%= pin.title %>">
      <h2><%= pin.title %></h2>
      <p class="user">Publicado por <%= pin.user.email %></p>
    </div>
  </div>
<% end %>
</div>
```

**Listado 16**. En `config/routes.rb`

```
root 'pins#index'
```

**Listado 17**. En `app/controllers/pins_controller.rb`

```
def new
  @pin = Pin.new
end
```

**Listado 18**. En `app/views/pins/new.html.erb`

```
<div class="container">
  <div class="row">
    <div class="col-sm-6 col-sm-offset-3">
      <h1>Nuevo Pin</h1>

      <%= form_for @pin do |f| %>
        <div class="form-group">
          <%= f.label :title %>
          <%= f.text_field :title, class: "form-control" %>
        </div>
        <div class="form-group">
          <%= f.label :image_url %>
          <%= f.url_field :image_url, class: "form-control" %>
        </div>

        <div class="action">
          <%= f.submit class: "btn btn-primary btn-lg btn-block" %>
        </div>
      <% end %>
    </div>
  </div>
</div>
```

**Listado 19**. En `app/controllers/pins_controller.rb`

```
def create
  pin = Pin.new(pin_params)
  pin.user = current_user
  if pin.save
    redirect_to root_path
  else
    render :new
  end
end

private
  def pin_params
    params.require(:pin).permit(:title, :image_url)
  end
```

**Listado 20**.

```
$ git add .
$ git commit -m 'Implementa la funcionalidad de listar y crear pines'
```

## Aplicando estilos

**Listado 21**. En `app/assets/stylesheets/application.scss`

```
body {
  background-color: #e9e9e9;
}

nav {
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.22);

  .navbar-brand {
    color: #bd1e23 !important;
    font-weight: bold;
    &:hover {
      text-decoration: none;
    }
  }
}

#pins {
  margin: 0 auto;

  .pin {
    margin: 10px;
    width: 350px;
    box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.22);
    border-radius: 7px;
    text-align: center;

    img {
      max-width: 100%;
      height: auto;
    }

    h2 {
      font-size: 22px;
      font-weight: 100;
      margin: 0;
      padding: 25px 10px;
      a {
        color: #474747;
      }
    }

    .user {
      font-size: 12px;
      border-top: 1px solid #eaeaea;
      padding: 15px;
      margin: 0;
    }

  }
}
```

**Listado 22**. En `app/views/layouts/application.html.erb`

```
<li><%= link_to "Nuevo Pin", new_pin_path %></li>
```

Algunos links a imágenes:

* https://s3.amazonaws.com/makeitreal/pins/lamborghini.jpg
* https://s3.amazonaws.com/makeitreal/pins/luxury-car.jpg
* https://s3.amazonaws.com/makeitreal/pins/office.jpg
* https://s3.amazonaws.com/makeitreal/pins/tianmen.jpg

Masonry: https://github.com/kristianmandrup/masonry-rails

**Listado 23**. En el archivo `Gemfile`.

```
gem 'masonry-rails'
```

**Listado 24**.

```
$ bundle install
```

**Listado 25**. En `app/assets/stylesheets/application.scss`

```
//= require 'masonry/transitions'
```

**Listado 26**. En `app/views/pins/index.html.erb`

```
<div id="pins" class="transitions-enabled clearfix masonry">
```

**Listado 27**. En `app/assets/javascripts/pins.coffee`

```
$ ->
  $('#pins').imagesLoaded ->
    $('#pins').masonry
      itemSelector: '.pin'
      isFitWidth: true
```

**Listado 28**.

```
$ git add .
$ git commit -m 'Aplica estilos CSS y configura Masonry'
```

### Publicando a Heroku

**Listado 29**.

```
$ heroku login
$ heroku create
```

**Listado 30**. En `Gemfile`

```
group :production do
  gem 'pg'
  gem 'rails_12factor'
end
```

**Listado 31**.

```
$ bundle install
$ git add .
$ git commit -m 'Configura Heroku'
$ git push heroku master
$ heroku run rake db:migrate
```

### Aplicar Bootstrap a las vistas Devise

**Listado 32**. En `app/views/devise/sessions/new.html.erb`

```
<div class="container">
  <div class="row">
    <div class="col-sm-6 col-sm-offset-3">
      <h2>Log in</h2>

      <%= form_for(resource, as: resource_name, url: session_path(resource_name)) do |f| %>
        <div class="form-group">
          <%= f.label :email %><br />
          <%= f.email_field :email, class: "form-control", autofocus: true %>
        </div>

        <div class="form-group">
          <%= f.label :password %><br />
          <%= f.password_field :password, class: "form-control", autocomplete: "off" %>
        </div>

        <% if devise_mapping.rememberable? -%>
          <div class="form-group">
            <%= f.check_box :remember_me %>
            <%= f.label :remember_me %>
          </div>
        <% end -%>

        <div class="actions">
          <%= f.submit "Log in", class: "btn btn-primary btn-block" %>
        </div>
      <% end %>

      <%= render "devise/shared/links" %>
    </div>
  </div>
</div>
```

**Listado 33**. En `app/views/devise/registrations/new.html.erb`

```
<div class="container">
  <div class="row">
    <div class="col-sm-6 col-sm-offset-3">
      <h2>Sign up</h2>

      <%= form_for(resource, as: resource_name, url: registration_path(resource_name)) do |f| %>
        <%= devise_error_messages! %>

        <div class="form-group">
          <%= f.label :email %><br />
          <%= f.email_field :email, class: "form-control", autofocus: true %>
        </div>

        <div class="form-group">
          <%= f.label :password %>
          <% if @minimum_password_length %>
          <em>(<%= @minimum_password_length %> characters minimum)</em>
          <% end %><br />
          <%= f.password_field :password, class: "form-control", autocomplete: "off" %>
        </div>

        <div class="form-group">
          <%= f.label :password_confirmation %><br />
          <%= f.password_field :password_confirmation, class: "form-control", autocomplete: "off" %>
        </div>

        <div class="actions">
          <%= f.submit "Sign up", class: "btn btn-primary btn-block" %>
        </div>
      <% end %>

      <%= render "devise/shared/links" %>

    </div>
  </div>
</div>
```

