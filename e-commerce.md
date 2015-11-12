# E-commerce

Taller de Bootstrap 3.

A continuación encontrarás los requisitos y listados de código para construir un e-commerce usando Bootstrap 3 y un poco de Ruby on Rails.

## Requerimientos

* Un editor de texto, nuestra recomendación es [Sublime Text](http://www.sublimetext.com/)
* Git, Ruby y Ruby on Rails. Si estás en Mac o Linux sigue las instrucciones en http://installrails.com/. Para Windows sigue las instrucciones en:
  * Git: https://makeitreal.wistia.com/medias/9jjnpri7lf
  * Ruby: https://makeitreal.wistia.com/medias/b85w0goonx
* Si no tienes esto intalado en tu máquina puedes utilizar https://c9.io/ que te provee con un entorno de desarrollo virtual.

Opcional:

* Crea una cuenta en [Github](https://github.com/).
* Crea una cuenta en [Heroku](http://heroku.com/).
* Descarga el [Heroku Toolbelt](https://toolbelt.heroku.com/).

## Listados

### Crear el proyecto

**Listado 0**.Crear archivo index.html

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Super Tienda</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.5/css/bootstrap.min.css">
  </head>
  <body>

  <h1>Hola Mundo</h1>
  <p>Bienvenido a la Super tienda</p>


  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.5/js/bootstrap.min.js"></script>
  </body>
</html>
```

**Listado 1**.

```
$ git init
$ git add .
$ git commit -m 'Versión inicial'
```

**Listado 2**.

```
$ git remote add origin git@github.com:[TU_USUARIO]/[TU_REPOSITORIO].git
$ git push origin master
```


### Configurar Bootstrap

Bootstrap: https://github.com/twbs/bootstrap-sass


**Listado 3**. En el archivo `Gemfile`.

```
gem 'bootstrap-sass', '~> 3.3.5'
```

**Listado 4**.

```
$ mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
```

**Listado 5**. En el archivo `app/assets/stylesheets/application.scss`

```
@import "bootstrap-sprockets";
@import "bootstrap";
// Y se eliminan las siguientes líneas:
*= require_tree .
*= require_self
```

**Listado 6**. En el archivo `app/assets/javascripts/application.js`

```
//= require bootstrap-sprockets
```

### Crear página de prueba

**Listado 7**.

```
$ touch app/controllers/pages_controller.rb
$ mkdir -p app/views/pages
$ touch app/views/pages/index.html.erb
```

**Listado 8**. En app/controllers/pages_controller.rb

```
class PagesController < ApplicationController
  def index
  end
end
```

**Listado 9**. En config/routes.rb

```
Rails.application.routes.draw do
  root "pages#index"
end
```

**Listado 10**. En app/views/pages/index.html.erb

```
<h1>Hola Mundo</h1>
<p>Bienvenidos al e-commerce</p>
```

**Listado 11**
```
git add —all
git commit -m "Configura bootstrap"
git push origin master
```


## Barra de navegación

**Listado 12**.

```
$ mkdir -p app/views/shared
$ touch app/views/shared/_navbar.html.erb
```

**Listado 13**. En app/views/shared/_navbar.html.erb

```
<nav class="navbar navbar-inverse">
  <div class="container">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-9" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">E-commerce</a>
    </div>
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-9">
      <div class="navbar-right">
        <ul class="nav navbar-nav">
          <li><a href="#"><span class="glyphicon glyphicon-shopping-cart"></span> Canasta</a></li>
          <li><a href="#">Salir</a></li>
        </ul>
      </div>
    </div>
  </div>
</nav>
```

**Listado 14**
```
$ touch app/assets/stylesheets/navbar.scss
```

**Listado 15**. En app/assets/stylesheets/navbar.scss

```
.navbar {
  border-radius: 0px;
}
```

**Listado 16**. En app/assets/stylesheets/application.scss

```
@import "navbar";
```

**Listado 17**

```
git add .
git commit -m "Agrega navbar"
git push origin master
```

## Entendiendo la grilla

**Listado 18**. En views/pages/index.html.erb

```
<div class="container">
    <div class="row">
        <div class="col-xs-3">
            Columna de 3
        </div>
        <div class="col-xs-3">
            Columna de 3
        </div>
        <div class="col-xs-6">
            Columna de 6
        </div>
        <div class="col-xs-4">
            Columna de 3
        </div>
        <div class="col-xs-8">
            Columna de 12
        </div>

        <div class="col-xs-12">
            Columna de 12
        </div>

        <div class="col-xs-1">
            Columna de 1
        </div>
        <div class="col-xs-1">
            Columna de 1
        </div>
        <div class="col-xs-1">
            Columna de 1
        </div>

    </div>
</div>
```

**Listado 19**. En app/assets/stylesheets/application.scss

http://sassmeister.com/
```
.row {
    @for $i from 1 through 12 {
      .col-xs-#{$i} {
        border-style: solid;
        border-color: red;
      }
    }
}
```

**Listado 20**. En views/pages/index.html.erb
```
<div class="col-xs-12 col-md-3"> Barra de búsqueda </div>
<div class="col-xs-12 col-md-9"> Carrusel </div>
```

## Barra de búsqueda

http://getbootstrap.com/components/#input-groups-buttons

**Listado 21**. En views/pages/index.html.erb
```
<div class="search-box">
   <div class="input-group">
        <input type="text" class="form-control" placeholder="Buscar camisetas">
        <div class="input-group-btn">
          <button class="btn btn-default" type="button"><span class="glyphicon glyphicon-search"></span></button>
        </div>
      </div>
 </div>
```

**Listado 22**
```
git add .
git commit -m "Agrega barra de busqueda"
git push origin master
```

## Filtro de categorías

**Listado 23**. En views/pages/index.html.erb

http://getbootstrap.com/components/#list-group
```
<div class="category-filter">
   <h4>Categorías</h4>
   <div class="list-group">
     <a href="#" class="list-group-item active">
       <span class="badge">14</span>
       Todos
     </a>
     <a href="#" class="list-group-item">
       <span class="badge">3</span>
       Mujer
     </a>
     <a href="#" class="list-group-item">
       <span class="badge">4</span>
       Hombre
     </a>
     <a href="#" class="list-group-item">
       <span class="badge">2</span>
       Hipster
     </a>
     <a href="#" class="list-group-item">
       <span class="badge">5</span>
       Universidad
     </a>
   </div>
 </div>
```

**Listado 24**. En app/assets/stylesheets/application.scss

```
.search-box {
   padding-bottom: 20px;
}
```

**Listado 25**. En views/pages/index.html.erb

http://getbootstrap.com/css/#responsive-utilities
```
<div class="category-filter hidden-xs hidden-sm">
```

**Listado 26**
```
git add .
git commit -m "Agrega filtro de categorías"
git push origin master
```

## Carrusel

http://getbootstrap.com/javascript/#carousel

**Listado 27**. En views/pages/index.html.erb
```
<div class=“carousel-container">
   <div id="carousel" class="carousel slide" data-ride="carousel">
     <!-- Indicators -->
     <ol class="carousel-indicators">
       <li data-target="#carousel" data-slide-to="0" class="active"></li>
       <li data-target="#carousel" data-slide-to="1"></li>
       <li data-target="#carousel" data-slide-to="2"></li>
     </ol>

     <!-- Wrapper for slides -->
     <div class="carousel-inner">
       <div class="item active">
         <img src="https://s3.amazonaws.com/makeitreal/projects/e-commerce/banner-slider-1.jpg">
       </div>
       <div class="item">
         <img src="https://s3.amazonaws.com/makeitreal/projects/e-commerce/banner-slider-2.jpg">
       </div>
       <div class="item">
         <img src="https://s3.amazonaws.com/makeitreal/projects/e-commerce/banner-slider-3.jpg">
       </div>
     </div>

     <!-- Controls -->
     <a class="left carousel-control" href="#carousel" role="button" data-slide="prev">
       <span class="glyphicon glyphicon-chevron-left"></span>
     </a>
     <a class="right carousel-control" href="#carousel" role="button" data-slide="next">
       <span class="glyphicon glyphicon-chevron-right"></span>
     </a>
   </div>
 </div>
```

**Listado 28**
```
git add .
git commit -m "Agrega carrusel"
git push origin master
```

## Lista de productos

**Listado 29**. En views/pages/index.html.erb

http://getbootstrap.com/components/#thumbnails

```
<div class="row">
   <% (1..5).each do |i| %>
     <div class="col-xs-6 col-sm-4">
       <div class="thumbnail">
         <img src="https://s3.amazonaws.com/makeitreal/projects/e-commerce/camiseta-<%= i %>.jpg">
         <div class="caption">
           <h3>Camiseta <%= i %></h3>
           <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore, dignissimos, architecto, facilis, optio sint veritatis similique ea laudantium eius accusantium eveniet quos sequi consequatur quam reiciendis harum voluptate cum recusandae!</p>
           <button class="btn btn-primary">$29 <span class="glyphicon glyphicon-shopping-cart"></span></button>
           <button class="btn btn-default">Detalles</button>
         </div>
       </div>
     </div>
   <% end %>
 </div>
```

**Listado 30**

```
git add .
git commit -m "Agrega lista de productos"
git push origin master
```
