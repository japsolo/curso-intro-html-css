# Clase V - Responsive Web Development - Mediaqueries y Frameworks

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
	+ [Slider](#sli)
	+ [Componentes](#com)
		+ [Botones](#btn)
		+ [Badgets](#bad)
		+ [Alerts](#ale)

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

Como vemos, Bootstrap usa un juego de `classes` de css que ya vienen creada y cada 


[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="nav"></a>
#### Navbars

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="sli"></a>
#### Slider

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="com"></a>
#### Componentes

<a name="btn"></a>
+ Botones

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<a name="bad"></a>
+ Badgets

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<a name="ale"></a>
+ Alerts

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)