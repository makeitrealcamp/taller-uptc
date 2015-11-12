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

