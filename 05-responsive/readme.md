# Capítulo V - Responsive Web Development - Mediaqueries y Frameworks

<a name="top"></a>

### Tabla de contenido

+ [Responsive Web Development](#rwd)
	+ [\<meta name="viewport">](#meta)
	+ [@media-queries](#queries)
	+ [min-width](#mnw)
	+ [max-width](#mxw)
+ [Bootstrap v3](#boot)
	+ [Vinculación (CDN vs local)](#link)
	+ [Sistema de Grillas](#grid)
	+ [Navbars](#nav)
	+ [Carrusel](#sli)
	+ [Componentes](#com)
		+ [Botones](#btn)
		+ [Badgets](#bad)
		+ [Alerts](#ale)
+ [*Volver al índice principal*](https://github.com/japsolo/curso-intro-html-css/) 

---

<a name="rwd"></a>
### Responsive Web Development

El **Responsive Web Development** se basa inicialmente en el desarrollo HTML/CSS de sitios web que se adapten a cualquier dispositivo. Pues como es bien sabido, hoy en día las/os usuarias/os consumen en su gran mayoría los sitios web desde sus dispositivos móviles (smartphones, tablets) y por lo tanto los mismos necesitan ajustarse a los requerimientos de tamaño del entorno de salida.

Por ello es que el **RWD** es un hito muy importante al momento de desarrollar un sitio web, pues si éste no cumple con los estándares esperados por cada usuaria/o se percibe que el mismo carece del uso de las últimas tecnologías del mercado.

Para comenzar a aplicar el **RWD** es necesario entender algunos conceptos base que veremos a continuación.

<br>

<a name="rwd"></a>	
#### \<meta name="viewport">

Lo primero que necesitamos para comenzar a aplicar el **RWD** es hacer uso de la siguiente etiqueta:

```html
<meta name="viewport">
```

Tal como lo vimos algunos capítulos anteriores, la etiqueta `<meta>` se encarga de proveer información al documento HTML y en este caso no es la excepción, pues al usar el atributo `name="viewport"` le estamos indicando al documento que queremos hacer algunas configuraciónes sobre el `viewport`. Ahora, lógicamente la pregunta que surge es ¿qué es el `viewport`?, veamos la respuesta a través de una imagen:

![alt text](./images/img01.jpg 'el viewport')

Viendo la imagen podemos decir que el `viewport` es el *puerto* o *área visual* de nuestro navegador en donde se muestran todos los elementos HTML del documento. Algo que es importante a tener el cuenta es:

+ El `viewport` está presente en TODOS los dispositivos pues hace parte inherente del navegador.
+ El `viewport` NO ES la resolución del dispositivo.

Ahora bien, para terminar de configurar nuestro documento HTML perfectamente, necesitamos configurar cómo queremos que el contenido del documento se comporte dentro del `viewport`, para ello vamos a implementar el atributo `content` así:

```html
<meta name="viewport" content="width=device-width">
```

Con el atributo `content` estamos definiendo que el ancho (`width`) de nuestro documento se deberá ajustar al ancho del dispositivo (`device-width`). Sencillo ¿no lo crees?

En conclusión, podemos decir que SIEMPRE que deseemos que el documento HTML se adapte al tamaño de ancho del `viewport` tendremos que implementar la etiqueta `<meta>` tal como la definimos anteriormente.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="rwd"></a>	
#### @media-queries

Ahora bien, el concepto inicial del **RWD** es el uso de la etiqueta `<meta>`. Sin embargo esto no es suficiente, pues más allá de lograr que el contenido del documento se ajuste al ancho del dispositivo, tenemos que generar que dicho contenido se adapte / re-organice según las condiciones de ancho del `viewport`. Veamos un ejemplo visual:

![alt text](./images/img02.png 'website adaptativo')

> Tal como lo vemos, el contenido (que siempre es el mismo) se re-organiza dependiendo del ancho del `viewport`. Con lo que logramos un sitio realmente sea RESPONSIVE.

En este sentido y para lograr este objetivo, CSS nos provee de las reglas `@media` también llamadas **media-queries**. Éstas reglas nos permiten agrupar un conjunto de sub-reglas de CSS, las cuales se aplicarán cuando se cumpla la condición de un determinado tamaño del `viewport`. En código se escribe así:

```css
@media (__viewport-size__) {
	// Sub-reglas CSS
}
```

En el anterior ejemplo vemos que hay un espacio que debemos rellenar: el **__viewport-size__**. En dicho lugar deberemos escribir el tamaño del `viewport` a partir del cual queremos implementar este conjunto de sub-reglas. Algo puntual a tener en cuenta, es que las sub-reglas que se implementan dentro del `@media` pueden ser reglas existentes las cuales deseemos modificar o nuevas reglas que deseemos implementar.

```css
body {
  background-color: olive;
}

@media (min-width: 640px) {
  body {
    background-color: yellow;
  }

  .main-title {
    font-size: 22px;
    color: orange;
  }
}
```

> El código anterior nos muestra que antes del media-querie existe la regla para el `body` la cual aplica el color de fondo `olive`. Luego, se define que cuando el `viewport` alcance como mínimo `640px` de ancho el `body` cambia su color de fondo a `yellow` y que adicionalmente se crea la regla `.main-title`.

Como vemos, un concepto clave a tener en cuenta al momento en que usamos las reglas `@media`, es el tamaño del `viewport` que queremos definir. Por ello, tenemos dos configuraciones posibles: `min-width` y `max-width` las cuales ampliaremos a continuación.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="mnw"></a>	
#### min-width

El valor `min-width` que se aplica en las reglas `@media` define que dicha regla se aplicara siempre y cuando se cumpla la condición de que el `viewport` tenga cómo mínimo ese tamaño en ancho o más. Si vemos este ejemplo:

```css
@media (min-width: 640px) {
  body {
    background-color: yellow;
  }

  .main-title {
    font-size: 22px;
    color: orange;
  }
}
```

Lo que estamos generando con esa regla `@media` es que SI el `viewport` tienen como **mínimo** 640px de ancho o más, el conjunto de reglas que se encuentran dentro de van a aplicar, en caso contrario, no se aplicarán.

Las reglas `@media` son bastante utilizadas con el `min-width` pues esto lo que nos permite generar es una aplicación web que sea **mobile first** ya que arrancamos desarrollando para las resoluciones más pequeñas y progresivamente vamos aumentando el re-acomodamiento de nuestro layout en función de un ancho mínimo de `viewport`.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="mxw"></a>
#### max-width

Ahora bien, así como tenemos la posibilidad de generar que nuestro layout se vaya ajustando desde un ancho mínimo del `viewport` hacia arriba, también contamos con la posibilidad de generar reglas `@media` que hagan lo contrario, es decir, que permitan que nuestro contenido se re-acomode siempre y cuando haya un tamaño máximo del `viewport` o menos. Veamos un ejemplo: 

```css
@media (max-width: 790px) {
  body {
    background-color: yellow;
  }

  .main-title {
    font-size: 22px;
    color: orange;
  }
}
```

El código anterior, generará que las reglas contenidas dentro del `@media` se apliquen solamente cuando el `viewport` tenga `790px` de ancho o menos. 

Algo importante a tener en cuenta es que **NUNCA** deberíamos aplicar reglas `@media` que mezclen `min-width` y `max-width` pues esto generará que algunas reglas se comiencen a pisar y será un caos completo.

La recomendación por temas de performance y demás es siempre arrancar a desarrollar desde **mobile first** y usar reglas `@media` con `min-width`.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

---

<a name="boot"></a>
### Bootstrap v3

Y bien, ya vamos llegando al final, pero ahora te estarás preguntando ¿y qué demonios es Bootstrap?. La respuesta corta sería: *es ua librería de CSS que trae un montón de reglas hechas para que las podamos usar libremente*. Lo mejor de todo es que es **GRATIS**. Es una libreria hecha por los creadores de Twitter y está muy copada.

Traduciendo literalmente la [documentación oficial](https://getbootstrap.com/docs/3.3/): *Bootstrap hace que el desarrollo de aplicaciones web sea más rápido y fácil. Se creó pensando en personas con todos los niveles de destrezas, dispositivos de todo tipo y proyectos de todos los tamaños.*

En otras palabras, *Bootstrap* es un set de reglas de CSS (y otras cositas más) que están agrupadas en una hoja de estilo que nos van a permitir hacer sitios web mucho más rápido y de manera más fácil. Cómo es lógico pensar, al ser Bootstrap una hoja de estilos que desarrollaron otras personas, vamos a necesitar SI o SI usar, tal como vienen definididas, las reglas css que dichas personas crearon para nosotros. Por ello es importante siempre que tengamos una duda de como usar algo, ir a la [documentación oficial](https://getbootstrap.com/docs/3.3/) y salir de la duda.

<br>

<a name="link"></a>
#### Vinculación (CDN vs local)

Existen dos maneras de comenzar a trabajar con Bootstrap en nuestro proyecto. La pimera de ellas (y no tan recomendada) es accediendo a la hoja de estilo de manera externa y la segunda accediendo a dicha hoja de estilo de de manera local.

```css
<link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
```
> Vinculación externa

```css
<link href="css/bootstrap.min.css" rel="stylesheet">
```
> Vinculación interna

Como vemos es bastante sencillo. Pues lo único que necesitamos es vincular la hoja de estilo de Bootstrap con nuestro proyecto. Y si quisieramos trabajar con Bootstrap de manera local (bajando el archivo a nuestro proyecto) lo único que tendremos que hacer es [descargar desde aquí los archivos](https://getbootstrap.com/docs/3.3/getting-started/).

Cuando descargemos los archivos vamos a ver una estructura de archivos así:

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css                // La única hoja de estilo que vamos a necesitar
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

Como vemos, son varios archivos, pero de momento solo usaremos uno de ellos `bootstrap.min.css`.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="grid"></a>
#### Sistema de Grillas

¿Sistema de grillas? Y esto ¿con qué acompañamiento se come? Seguramente te estarás preguntando. Y bueno, es algo que Bootstrap nos ofrece y lo que lo hace realmente maravilloso pues Bootstrap incluye este sistema que es pensado para móviles y que cumple con el desarrollo web responsive. Este **grid system** está compuesto de filas y columnas, columnas que van creciendo progresivamente dependiendo del ancho del `viewport`.

Algo importante a tener en cuenta es que dentro de una fila pueden llegar a caber como máximo 12 columnas, pero veamos mejor algo gráfico:

![alt text](./images/img03.png 'grid system')
![alt text](./images/img04.jpg 'grid system')

Como lo vemos, al usar un sistema de grilla lo que estamos logrando de manera visual es un layout mucho más consistente y homogéneo que sea más sencillo de ordenar.

Ahora bien, cómo funciona esto en bootstrap, veamos la siguiente tabla:

|   | XS devices (<768px) | SM devices (≥768px) | M devices (≥992px) | L devices (≥1200px) |
|---|:---:|:---:|:---:|:---:|
| Prefijo de Clase | `.col-xs-` | `.col-sm-` | `.col-md-` | `.col-lg-` | 

Como vemos, Bootstrap usa un juego de `classes` de css que ya vienen creadas y cada una de ellas se aplicará dependiendo del ancho que tenga el `viewport`. Por ejemplo, si aplicamos el siguiente juego de clases `class="col-xs-6 col-sm-3"` estamos ordenándole a un contenedor que ocupe 6 columnas (de las 12 posibles), cuando el ancho del `viewport` se encuentre por debajo de `767px` y a su vez que ocupe 3 columnas desde que el `viewport` tenga como ancho un mínimo de `768px` hacia arriba. Un ejemplo más concreto en código sería el siguiente:

```html
<div class="row">
  <div class="col-xs-12 col-sm-6 col-md-8">.col-xs-12 .col-sm-6 .col-md-8</div>
  <div class="col-xs-6 col-md-4">.col-xs-6 .col-md-4</div>
</div>
<div class="row">
  <div class="col-xs-6 col-sm-4">.col-xs-6 .col-sm-4</div>
  <div class="col-xs-6 col-sm-4">.col-xs-6 .col-sm-4</div>
  <div class="col-xs-6 col-sm-4">.col-xs-6 .col-sm-4</div>
</div>
```

Lo anterior se vería en pantalla más o menos así:

> Cuando el `viewport` tiene menos de 768px de ancho

![alt text](./images/img06.jpg 'grid system bootstrap')

> Cuando el `viewport` tiene como mínimo 768px de ancho o más

![alt text](./images/img07.jpg 'grid system bootstrap')

> Cuando el `viewport` tiene como mínimo 992px de ancho o más

![alt text](./images/img05.jpg 'grid system bootstrap')

Ahora bien, como te das cuenta, todas las `.col-` siempre van contenidas dentro de un elemento con clase `row` pues dicho elemento contenedor evita que las columnas se desborden y que nuestro *layout* se ve mal. Por ello siempre debés recordar la siguiente estructura:

```html
<div class="container">
  <div class="row">
    <!-- Aquí dentro van las columnas -->
  </div>
</div>
```

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="nav"></a>
#### Navbars

Otro elemento interesante que nos provee bootstrap son las `nav-bar` o tal como su nombre lo indica, las barras de navegación. Y si, bootstrap ya tiene una solución lista para nosotros. Veamos primero el siguiente ejemplo:

![alt text](./images/img07.gif 'bootstrap navbar')

¡Maravilloso! ¿no es así?. Como lo vemos, bootstrap ya solucionó, no solo el tema de una barra de navegación adaptable, si no que a su vez logro hacer funcional el evento de ocultar la misma cuando el tamaño de ancho del `viewport` es inferior a los `768px`. Ahora bien ¿cómo es posible esto?. Inspeccionemos el código fuente:

```html
<nav class="navbar navbar-default">
  <div class="container-fluid">

    <!-- Logo e ícono de navegación en mobile -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#myNav">
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">Logo</a>
    </div>

    <!-- Navbar links -->
    <div class="collapse navbar-collapse" id="myNav">
      <ul class="nav navbar-nav">
        <li class="active"><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown">
            Services<span class="caret"></span>
          </a>
          <ul class="dropdown-menu">
            <li><a href="#">Service 01</a></li>
            <li><a href="#">Service 02</a></li>
            <li><a href="#">Service 03</a></li>
          </ul>
        </li>
      </ul>
    </div>

  </div>
</nav>
```

Primero que todo, podemos ver que existe un elemento contenedor con las clases `navbar navbar-default`, el mismo es indispensable para generar toda la barra de navegación en si. Luego, nos encontramos con un elemento con clase `container-fluid`, el mismo genera que la barra de navegación ocupe siempre todo el ancho del `viewport`. Después tenemos en si dos bloque grandes de elementos que componen la *navbar*, por un lado tenemos al elemento con clase `navbar-header` que tiene dentro por un lado el logotipo / marca y por otro el famoso ícono de la *hamburguesa* o las tres líneas que representan un botón que al estar en una resolución de dispositivo móvil, desplegará la barra de navegación completa.

Por otro lado tenemos al elemento con las clases `collapse navbar-collapse` el cual es en si los enlaces de la barra de navegación y vemos que dentro tiene un lista tradicional con los enlaces necesarios. Ahora bien, algo importante a tener en cuenta son dos cosas. La primera de ella es la conexión que existe entre el botón que despliega la barra de navegación. Si vemos el elemento con clases `navbar-toggle collapsed` vemos que el mismo tiene un atributo `data-target` con el valor `#myNav`, la segunda cosa a tener en cuenta es que el elemento con clases `collapse navbar-collapse` tiene un atributo `id` con el valor `myNav`. La conexión entre estos dos es evidente y básicamente lo que permite es que al hacer clic sobre el botón `navbar-toggle collapsed` se despliege (si está oculta) la lista de enlaces `collapse navbar-collapse`.

Ahora bien, lo anteriormente mencionado no sería posible sin vincular unas librerias de **JavaScript** necesarias para el funcionamiento de este comportamiento. Lo único que tenemos que hacer en nuestro documento HTML es insertar lo siguiente:

```html
<!-- jQuery (necesaria para los plugins de JavaScript de Bootstrap's) -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>

<!-- Para implementar las funcionalidades de los eventos y demás -->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
```

Realmente la implementación de este tipo de elementos que nos da la librería de bootstrap es relativamente sencilla y entre más lo practiquemos más vamos a entender su funcionamiento de una manera completa.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="sli"></a>
#### Carrusel

Otro de los maravillosos elementos que nos da la librería de bootstrap es el **carrusel** que bien puede ser de solo imágenes o de cualquier tipo de contenido. Veamos un ejemplo:

![alt text](./images/img08.gif 'bootstrap carousel')

Sorprendente ¿no te parece? Pues bien, este tipo de elemento requiere también de las librerias de **JavaScript** mencionadas en las **Navbars** así que daremos por sentado que esto está entendido perfectamente, por lo que nos concentraremos en la estructura HTML. Si vemos el siguiente código:

```html
<div class="carousel slide" id="myCarousel">
  <!-- Puntitos Indicadores -->
  <ol class="carousel-indicators">
    <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
    <li data-target="#myCarousel" data-slide-to="1"></li>
    <li data-target="#myCarousel" data-slide-to="2"></li>
  </ol>

  <!-- Contenedor de cada slide -->
  <div class="carousel-inner">
    <div class="item active">
      <img src="..." alt="...">
    </div>
    <div class="item">
      <img src="..." alt="...">
    </div>
    <div class="item">
      <img src="..." alt="...">
    </div>
  </div>  

  <!-- Controles -->
  <a class="left carousel-control" href="#myCarousel" data-slide="prev">
    <span class="glyphicon glyphicon-chevron-left"></span>
  </a>
  <a class="right carousel-control" href="#myCarousel" data-slide="next">
    <span class="glyphicon glyphicon-chevron-right"></span>
  </a>
</div>
```

En la estructura anterior claramente podemos identificar 3 elementos importantes. Los **indicadores** (`carousel-indicators`), el **contenido de cada slide** (`carousel-inner`) y los **controles** anterior / siguiente (`carousel-control`). 

Algo importante a tener en cuenta es el uso de un elemento contenedor general del grupo anteriormente mencionado, dicho contenedor lleva la clase `carousel slide` y el `id="myCarousel"`. Este último bastante importante pues como te das cuenta en varios lugares (indicadores y controles) del código se hace referencia al mismo.

Adicionalmente el contenido que deseamos mostrar en cada slide irá en el contenedor `carousel-inner` dentro de un sub-contenedor con clase `item`. Dentro de dicho elemento es donde iran las imágenes `<img>` de nuestro carrusel. ¿Sencillo no?.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="com"></a>
#### Componentes

Dentro de todos los elementos que tiene bootstrap hay una clara sección de *componentes*, que no son otra cosa más que un set de diversos elementos estilizados que podremos usar según como lo necesitemos. A continuación veremos los más comunmente utilizados.

<a name="btn"></a>
+ Botones

Siempre que necesitemos de un botón para cualquier instancia de nuestra aplicación, podremos recurrir al set de botones que nos provee bootstrap, pues los mismos ya están estilizados de una manera tal en donde por medio del color otorgamos un significado a cada uno de ellos. Veamos:

![alt text](./images/img08.jpg 'botones de bootstrap')

Interesante ¿no es así? Ahora bien veamos los fácil que es implementar los mismos en nuestro HTML, pues lo único que necesitaremos es implementar un par de clases en cada elemento así:

```html
<!-- Botón estandard -->
<button type="button" class="btn btn-default">Default</button>

<!-- Botón de acción primaria -->
<button type="button" class="btn btn-primary">Primary</button>

<!-- Botón para indicar una acción exitosa -->
<button type="button" class="btn btn-success">Success</button>

<!-- Botón para indicar información a tener en cuenta -->
<button type="button" class="btn btn-info">Info</button>

<!-- Botón para indicar un evento sobre el cual hay que tener precaución -->
<button type="button" class="btn btn-warning">Warning</button>

<!-- Botón para indicar un evento peligroso -->
<button type="button" class="btn btn-danger">Danger</button>

<!-- Botón que parece un enlace pero cumple el papel de ser un botón -->
<button type="button" class="btn btn-link">Link</button>
```

Adicionalmente estos botones pueden ser personalizados en tamaño ¿cómo? a través de una clase adicional que puede ser `.btn-lg`, `.btn-sm`, ó `.btn-xs`.

```html
<p>
  <button type="button" class="btn btn-primary btn-lg">Large button</button>
  <button type="button" class="btn btn-default btn-lg">Large button</button>
</p>
<p>
  <button type="button" class="btn btn-primary">Default button</button>
  <button type="button" class="btn btn-default">Default button</button>
</p>
<p>
  <button type="button" class="btn btn-primary btn-sm">Small button</button>
  <button type="button" class="btn btn-default btn-sm">Small button</button>
</p>
<p>
  <button type="button" class="btn btn-primary btn-xs">Extra small button</button>
  <button type="button" class="btn btn-default btn-xs">Extra small button</button>
</p>
```

> El anterior código se vería así:

![alt text](./images/img09.jpg 'botones de bootstrap')

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<a name="bad"></a>
+ Badgets

No hay mejor manera de explicar un `badget` que de una forma visual, así que veamos:

![alt text](./images/img10.jpg 'badge de bootstrap')

Quizás estés familiarizado con este tipo de recursos visual ¿no? `badge` traduce literalmente *distintivo* y básicamente es un pequeño, pero importante, elemento que nos permite notificar al usuario principalmente de una cantidad de mensajes recibidos y sin leer. La implementación es realmente sencilla pues solamente deberás hacer lo siguiente:

```html
<a href="#">Inbox <span class="badge">42</span></a>

<button class="btn btn-primary">
  Messages <span class="badge">4</span>
</button>
```

Lo importante del código anterior es el uso de `<span class="badge">...</span>`. Pues es lo único necesario para comenzar a mostrar este tipo de alertas. Cool ¿no te parece?.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<a name="ale"></a>
+ Alerts

Las alertas son otro recurso bastante sencillo de bootstrap y básicamente nos sirven para mostrar textos llamativos al usuario, veamos:

![alt text](./images/img11.jpg 'alert de bootstrap')

Como te das cuentas, una alerta no es otra cosa más que un bloque de texto con un color de fondo y tipografía determinados. Lo anterior, en código se ve así:

```html
<p class="alert alert-success">...</p>
<p class="alert alert-info">...</p>
<p class="alert alert-warning">...</p>
<p class="alert alert-danger">...</p>
```

Es evidente que las alertas son levemente parecidas a los botones, pues dependiendo de la clase que apliquemos obtendremos un bloque de texto llamativo según el caso.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

---

**Made with ❤️ by: [Javi Herrera](https://javier-herrera.com)**

*Si te parece interesante este tipo de contenido, puedes agradecerme con un Follow en mis siguientes redes sociales. Lo estimaría un montón.*

[![icon linkedin](../images/icon-linkedin.png)](https://www.linkedin.com/in/japsolo/)
[![icon instagram](../images/icon-instagram.png)](https://www.instagram.com/thefullstackdevs/)
[![icon spotify](../images/icon-spotify.png)](https://open.spotify.com/show/3J2dLuBSfzt9VVnEF8q18a)