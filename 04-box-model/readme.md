# Capítulo IV - Selectores avanzados, Modelo de cajas y Posicionamiento 
<a name="top"></a>

### Tabla de contenido

+ [Selectores avanzados de CSS](#sel-ava)
  + [Universal](#univ)
  + [Descendente](#des)
  + [Hijos directos](#child)
+ [Pseudo selectores de CSS ](#pseudo)
  + [:visited](#vis)
  + [:hover](#hov)
  + [:active](#act)
  + [:focus](#foc)
+ [Modelo de caja](#box)
  + [display](#dis)
  + [width & height](#w&h)
  + [padding](#pad)
  + [border](#bor)
  + [margin](#mar)
  + [box-sizing](#bsz)
  + [border-radius](#bra)
+ [Posicionamiento](#pos)
  + [float](#flo)
  + [relative](#rel)
  + [absolute](#abs)
  + [fixed](#fix)
+ [*Volver al índice principal*](https://github.com/japsolo/curso-intro-html-css/) 

---

<a name="sel-ava"></a>
### Selectores avanzados de CSS

Hasta el momento hemos visto un par de selectores de CSS que nos permiten asignar reglas de estilo de varias formas. Si embargo, tal como lo mencionamos en su momento, no son los únicos selectores existentes pues hay algunos otros más que nos dan la posibilidad de implementar reglas de CSS según lo necesitemos. Veamos los mismos.

<br>

<a name="univ"></a>
#### Universal

El **selector universal**, es un selector especial, pues podríamos decir que *solo lo podemos usar una vez*. Pues el objetivo del mismo, es asignar declaraciones CSS a **TODOS** los elementos HTML. Lo cual trae consigo un gran poder, pero *con todo gran poder viene una gran responsabilidad*. ¿Como se aplica este selector? Veamos un ejemplo:

```css
* {
  /* declaraciones CSS */
}
```

Como vemos en el código, el asterisco (`*`) es el símbolo utilizado para definir ésta regla. Vale la pena aclarar que este selector forma parte de algunos *hacks* muy utilizados, como lo veremos más adelante.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="des"></a>
#### Descendente

El **selector descendente** asigna estilo a todos los elementos de cierto tipo que se encuentran dentro de otro elemento. Un elemento es descendente de otro cuando se encuentra dentro de las etiquetas de apertura y de cierre del otro elemento. Veamos un ejemplo:

```css
.container a {
  color: green;
}
```

En el código anterior, estamos seleccionando todos los elementos `<a>` que se encuentren dentro de un elemento con clase `container`. Si nuestro código HTML fuera así:

```html
<div class="container">
  <a href="contacto.html">Contáctanos</a>
  ...
  <p><a href="http://www.twitter.com">Síguenos en Twitter</a></p>
  ...
</div>
```

El selector descendente, daría estilo al elemento `<a>` con texto **Contáctanos** pero así mismo también al `<a>` con texto **Síguenos en Twitter**, por más que este último se encuentre dentro de un elemento `<p>`. En otras palabras podríamos decir que cualquier elemento `<a>`que esté dentro de un elemento con clase `container` tomará el estilo definido en dicha regla.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="child"></a>
#### Hijos directos

El selector de **Hijos directos** es algo similar al selector **Descendente**, pero a su ves muy diferente en su funcionamiento. Se utiliza para seleccionar un elemento HTML que se encuentra de manera DIRECTA dentro de otro elemento HTML. Este selector se indica mediante el _"signo mayor que"_ (`>`). Tomemos el ejemplo del selector anterior, pero ahora haciendo que este selector:

```css
.container > a {
  color: green;
}
```

Ahora, en el código anterior estamos seleccionando SOLAMENTE los elementos `<a>` que sean hijos directos de elemento con clase `container`. Teniendo en cuenta que el código HTML es así:

```html
<div class="container">
  <a href="contacto.html">Contáctanos</a>
  ...
  <p><a href="http://www.twitter.com">Síguenos en Twitter</a></p>
  ...
</div>
```

El selector de **Hijos directos** solamente da estilo al elemento `<a>` con texto **Contáctanos** y no al elemento `<a>` con texto **Síguenos en Twitter** pues éste último es hijo directo del elemento `<p>`.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

---

<a name="pseudo"></a>
### Pseudo selectores de CSS

Los Pseudo selectores son selectores que se suelen aplicar sobre otro selector y se utilizan para poder modificar un comportamiento determinado. La sintaxis de un pseudo-selector contiene el signo `:` seguido del nombre del pseudo-selector, algo más o meno así: `:nombre-pseudo-selector`.

Algunos de estos pseudo-selectores se pueden aplicar a cualquier elemento HTML, mientras que algunos otros solamente se aplican a algunos elementos HTML. Veamos entonces los siguientes.

<br>

<a name="vis"></a>
#### :visited

El pseudo-selector `:visited` se utiliza para aplicar estilo a los elementos de enlace (`<a>`) que han sido visitados al menos una vez por las/os usuarias/os de nuestro sitio web. 

```css
a {
  color: green;
}

a:visited {
  color: gray;
}
```

El código anterior aplica a los elementos de enlace que no han sido visitados un color *verde* y a los enlaces visitados un color *gris*. Como lo vemos, si leemos con detalle el código, podemos de manera intuitiva deducir qué está haciendo el mismo, sencillo ¿no te parece?.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="hov"></a>
#### :hover

El pseudo-selector `:hover` se activa cuando el usuario pasa el cursor del mouse sobre un elemento de enlace. Vale hacer la aclaración que este pseudo-selector también puede ser aplicado en cualquier otro elemento HTML, no solamente a los enlaces.

```css
a {
  color: green;
  text-decoration: none;
}

a:hover {
  color: orange;
  text-decoration: underline;
}

.warning-text:hover {
  color: red;
  background-color: yellow;
}
```

El código anterior genera que al pasar el cursor del mouse sobre un enlace, el mismo tome color tipográfico naranja y texto subrayado. Y así mismo, permite que al pasar el cursor sobre un elemento con clase `warning-text` el mismo aplique color rojo a la tipografía y color de fondo amarillo.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="act"></a>
#### :active

El pseudo-selector `:active`, se aplica cuando hacemos click sobre un elemento de enlace. Éste estilo se aplica durante un periodo de tiempo casi imperceptible, ya que dura desde que se pulsa el botón del mouse hasta que se libera. Si quisieramos verlo en funcionamiento por un periodo de tiempo más prolongado, tendríamos que dejar presionado el botón del mouse por unos cuantos segundos.

```css
a:active {
  color: white;
  background-color: red;
}
```

El código anterior permite que al hacer click sobre un enlace, el mismo tome un color de fondo rojo y un color tipográfico blanco.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="foc"></a>
#### :focus

El pseudo-selector `:focus` se aplica cuando un elemento HTML tiene el foco del cursor, es decir, cuando el cursor se encuentra dentro de dicho elemento. Normalmente se aplica a los elementos `<input>` de los formularios cuando éstos mismos tienen el cursor dentro y por lo tanto se puede escribir directamente en esos campos.

```css
input:focus {
  color: orange;
  font-weight: bold;
}
```

El código anterior generará que cuando un elemento `<input>` tenga el cursor dentro de si, el texto se torne de color naranja y que a su vez el trazado de la tipografía sea bold.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

---
<a name="box"></a>
### Modelo de caja

El modelo de caja o también llamado *box-model*, es un concepto **muy importante** en CSS pues el mismo nos permite implementar un set de propiedades a los elementos de HTML y en función de ello setear varias características como un relleno, bordes, márgenes, etc.

Lo primero que necesitamos es entender que **TODOS** los elementos del HTML generan una **CAJA**, es decir, generan cuatro costados con los cuales podemos trabajar. Veamos gráficamente como sería:

![alt text](./images/img01.gif 'box model')

Entendiendo lo anterior, podemos pasar entonces a las propiedades que nos permiten setear las características mencionadas con anterioridad.

<br>

<a name="dis"></a>
#### display

Esta propiedad es bastante importante, pues nos permite definir el comportamiento de cualquier elemento de HTML. Lo primero a entender de esta propiedad, es que por defecto, cada etiqueta de HTML tiene un comportamiento default, el cual puede ser cambiado a nuestro antojo según lo deseemos.

Los 4 valores más importantes de la propiedad `display` son: 

+ `inline`: se considera que un elemento es *de línea* cuando el mismo a lo ancho, solamente ocupa el ancho correspondiente a su contenido interno. Viendo la siguiente imagen:

![alt text](./images/img02.jpg 'display inline')

Podemos decir que cualquier elemento HTML que permite ubicarse en sus costados laterales a otros elementos HTML es considerado **de línea**. Una de las particularidades de este tipo de elemento es que no puede recibir algunas de las propiedades de *box model* como por ejemplo `width`, `height`, `margin`, entre otras. Su aplicación en CSS será así:

```css
display: inline;
```

+ `block`: se considera que un elemento es *de bloque* cuando el mismo a lo ancho, independientemente del tamaño que se le asigne ocupa todo el espacio sobrante a sus costados, generando que cualquier otro elemento se ubique por encima o debajo de éste. Viendo la siguiente imagen:

![alt text](./images/img03.jpg 'display block')

Podemos visualizar el comportamiento de los elementos e ir entendiendo los conceptos del *box model*. Una particularidad de los elementos **de bloque** es que SI reciben propiedades `width`, `height`, `margin`, entre otras y si no tienen definido un ancho específico, su ancho será igual al 100% que el de su elemento padre. Su aplicación será así:

```css
display: block;
```

+ `inline-block`: se considera que un elemento es *de línea-bloque* cuando el mismo toma los dos conceptos anteriores y los fusiona en un solo, pues por un lado permite que otros elementos de *línea* o *línea-bloque* se ubiquen a sus costados laterales y recibe propiedades del *box model* como por ejemplo `width`, `height`, `margin`, etc. Viendo la siguiente imagen:

![alt text](./images/img04.jpg 'display inline-block')

Podemos deducir fácilmente el comportamiento de este tipo de elementos. Su aplicación será así:

```css
display: inline-block;
```

+ `none`: éste es otro valor que podemos aplicar en la propiedad `display`. Y lo que genera es que un elemento quede oculto y no se muestre en el navegador. Generalmente es utilizado para hacer que un elemento esté oculto desde que se cargue el documento y que el mismo solamente se muestre si el usuario ejecuta un evento tipo `:hover`. Un ejemplo claro de este recurso son las barras de navegación desplegables.

![alt text](./images/img05.gif 'display none')

Su implementación es CSS será así:

```css
display: none;
```

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="w&h"></a>
#### width & height

Una de las particularidades del *box model* es la posibilidad que tenemos de aplicar tamaño (ancho y alto) a un elemento **de bloque** o **de línea-bloque**. Pera ello, CSS nos provee de las propiedades `width` y `height`, las cuales no permite implentar el tamaño deseado.

+ `width`: ésta propiedad recibe como valor un número expresado en `px` (pixeles) o `%` (porcentaje) y el mismo define el ancho que ocupara el elemento. Veamos unos ejemplos: 

```css
.box-A {
  width: 450px;
}

.box-B {
  width: 70%;
}
```

En el código anterior, tenemos dos reglas *de tipo clase*: `.box-A` y `.box-B`. La primera `.box-A` define que el ancho del elemento será `450px`, mientras que la segunda `.box-B` define que el ancho del elemento será `70%`. Ahora bien, la diferencia entre los `px` y los `%` es que la primera unidad de medida, es considerada una *unidad de medida absoluta* pues independientemente del contexto su ancho siempre será el mismo. Mientras que la segunda unidad de medida se considera una *unidad de medida relativa* pues ésta posee la facultad de cambiar en función de su contexto, por ejemplo, si el contenedor padre de éste elemento cambia de tamaño a lo ancho, éste contenedor se ajustará al mismo y ocupará lo correspondiente asignado en el `width`.

![alt text](./images/img06.gif 'pixeles vs porcentajes') 

+ `height`: ésta propiedad nos permite definir el alto de un elemento. La misma recibe un valor númerico que preferiblemente debe estar expresado en `px` pues si aplicamos `%` no funcionará como esperamos. Algo a tener en cuenta con esta propiedad, es que hoy en día suele ser poco utilizada, pues generalmente vamos a querer que nuestros contenedores se ajustes, a lo alto, a su contenido interno y si definieramos un `height` para dicho contenedor, su alto sería estático y provocaría que si el contenido interno es superior éste rebalsaría fuera del contenedor padre.

![alt text](./images/img07.jpg 'alto del contenedor') 

Su implementación sería así:

```css
.box-A {
  height: 450px;
}

.box-B {
  height: 150px;
}
```

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="pad"></a>
#### padding

La propiedad `padding` nos permite definir un determinado espacio de **relleno interno** el cual se aplicará desde los bordes del elemento hacia adentro. Recibe de uno hasta 4 valores numéricos expresados en `px`.

![alt text](./images/img08.jpg 'padding - relleno') 

Como vemos en el ejemplo anterior, al aplicar `padding` el contenido del elemento se ve cercado por un espaciado entre él y los bordes de su caja. Esta práctica es bastante comun cuando queremos generar este tipo de *espaciado interno* dentro de un elemento. Su aplicación será así:

```css
/* caja con mismo padding en los 4 costados */
.box {
  padding: 15px;
}

/* caja con mismo padding en top/bottom y mismo padding en right/left */
.box {
  padding: 15px 30px;
}

/* caja con padding 15px en top, mismo padding en right/left y 0 en bottom*/
.box {
  padding: 15px 30px 0;
}

/* caja con padding 15px en top, padding 30px en right, padding 0 en bottom y padding 40px en left*/
.box {
  padding: 15px 30px 0 40px;
}
```

Como vemos en el código anterior, si necesitaramos aplicar 2, 3 ó 4 valores, los mismos son separados por un espacio y tomarían el siguiente órden:

![alt text](./images/img09.jpg 'orden de aplicación del padding')

Es importante tener en cuenta que cuando aplicamos `padding`, **el valor asignado se sumará** a los valores definidos en `width` y `height`.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="bor"></a>
#### border

La propiedad `border` nos permite implementar un línea decorativa a cualquier elemento HTML. La misma está compuesta de 3 características:

+ `style`: define el estilo de la línea, aquí hay 3 valores posibles `solid` (línea continua), `dashed` (línea discontinua de guiones) y `dotted` (línea discontinua de puntos).
+ `width`: ancho de la línea/borde, su valor se aplica en `px`.
+ `color`: color de la línea/borde, el valor puede ser definido en cualquier formato de color aceptado por CSS.

Su aplicación sería:

```css
/* borde sólido de 3px de color rojo */
.box-1 {
  border: solid 3px #ff0000;
}

/* borde discontinuo de guiones de 5px de color verde */
.box-2 {
  border: dashed 5px #00ff00;
}

/* borde discontinuo de puntos de 2px de color azul */
.box-2 {
  border: dotted 2px #0000ff;
}
```

![alt text](./images/img10.jpg 'tipos de borde')

Al igual que con el `padding`, es importante tener en cuenta que cuando aplicamos `border`, **el valor asignado se sumará** a los valores definidos en `width` y `height`.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="mar"></a>
#### margin

La propiedad `margin` nos permite aplicar una determinada cantidad de distanciamiento entre los elementos. Dicho distanciamiento se aplica desde los bordes hacia afuera y recibe un valór numérico expresado en `px` ó `%`. Si bien no afecta en si el tamaño del elemento, sí ocupa espacio dentro del entorno de elementos que lo rodean. Su aplicación es muy parecida al `padding`.

```css
/* caja con mismo margin en los 4 costados */
.box {
  margin: 15px;
}

/* caja con mismo margin en top/bottom y mismo margin en right/left */
.box {
  margin: 15px 30px;
}

/* caja con margin 15px en top, mismo margin en right/left y 0 en bottom*/
.box {
  margin: 15px 30px 0;
}

/* caja con margin 15px en top, margin 30px en right, margin 0 en bottom y margin 40px en left*/
.box {
  margin: 15px 30px 0 40px;
}
```

Viendo un panorama general, la siguiente imagen nos da una idea completa de como trabajan el `width`, `heigth`, `padding`, `border` y `margin`.

![alt text](./images/img11.jpg 'modelo de caja completo')

A este esquema es lo que tradicionalmente conocemos y llamamos el **Modelo de Cajas**. Algo que tal como lo mencionamos en su momento es demasiado importante de conocer si queremos ser excelentes *coders* de CSS.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="bsz"></a>
#### box-sizing

Como ya lo definimos en las propiedades vistas con anterioridad. Una de las particularidades de aplicar las propiedades del **modelo de caja**, es que las mismas afectan directamente el tamaño final de un elemento. Por lo tanto CSS nos da una propiedad que evita que al aplicar `padding` y `border` dichos valores se sumen al tamaño definido para la caja en `width` y `height`.

El `box-sizing`, es una propiedad de dos únicos valores: `content-box` y `border-box`. Su valor default es `content-box` y el mismo genera que `padding` y `border` se sumen a `width` y `height`. Ahora bien, si quisieramos que `padding` y `border` *NO SE SUMARAN* a `width` y `height` tendríamos que aplicar el valor `border-box`.

Una técnica muy usual suele ser la siguiente:

```css
* {
  box-sizing: border-box;
}
```

Pues tal como lo vimos más arriba, el selector universal `*` nos permite aplicar declaraciones CSS a todos los elementos del HTML, por lo tanto nuestro código anterior nos permite definir un comportamiento en donde cuando sea que apliquemos `padding` y `border` los mismos *NO SE SUMARAN* al `width` y `height` del elemento. Veamos la siguiente imagen:

![alt text](./images/img12.jpg 'box-sizing')

Excelentísimo recurso ¿no te parece?

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="bra"></a>
#### border-radius

La propiedad `border-radius` nos permite asignar una determinada cantidad de redondez a las esquinas de una caja. Algo que está bastante *cool* pues dicho recurso permite hacer que nuestros elementos no siempre estén tradicionalmente con esquinas angulares. El valor asignado en esta propiedad puede ser un valor numérico en `px` o `%` y se admiten de 1 a 4 valores. Veamos:

```css
/* todas las esquinas de la caja con 15px de redondez */
.box-1 {
  border-radius: 15px;
}

/* 
  esquinas superior izquierda e inferior derecha con 5px de redondez
  esquinas superior derecha e inferior izquierda con 30px de redondez
*/
.box-2 {
  border-radius: 5px 30px;
}

/* 
  esquina superior izquierda con 15px de redondez
  esquinas superior derecha e inferior izquierda con 30px de redondez
  esquina inferior derecha con 0 de redondez
*/
.box-3 {
  border-radius: 15px 30px 0;
}

/* 
  esquina superior izquierda con 15px de redondez
  esquinas superior derecha con 30px de redondez
  esquina inferior derecha con 0 de redondez
  esquina inferior izquierda con 50px de redondez
*/
.box-4 {
  border-radius: 15px 30px 0 50px;
}
```

![alt text](./images/img13.jpg 'border-radius')

Otro efecto que podríamos lograr es un círculo perfecto, esto siempre y cuando el elemento posea el mismo valor en ancho y alto.

```css
.box {
  width: 150px;
  height: 150px;
  border-radius: 50%;
}
```

![alt text](./images/img14.jpg 'border-radius')

Maravilloso, ¿no te parece?.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

---

<a name="pos"></a>
### Posicionamiento

Cuando hablamos de posicionamiento en CSS, nos referimos a la manera en que podemos disponer los elementos de nuestros HTML para que entre ellos exista una fluidez y así mismo podamos generar *layouts* de cualquier tipo. Como por ejemplo:

![alt text](./images/img15.jpg 'web layout')

En la anterior imagen podemos ver que algunos elementos se posicionan junto a otros de una manera particular y hasta el momento desconocida para nosotros. Pues bien, las siguiente propiedades buscan que podamos lograr resultados similares a los que nos ilustra la imagen. Veámoslos entonces.

<br>

<a name="flo"></a>
#### float

EL posicionamiento por flotación es uno de los más utilizados, pues no permite hacer que un elemento se posicione justo al lado de otro elemento. La propiedad usada es `float` y recibe uno de los siguientes 3 valores: `none` (default), `left`, `right`. Si entendemos que por default, los elementos *de bloque* se posicionan uno debajo del otro:

![alt text](./images/img16.jpg 'posicionamiento default')

Podríamos entonces hacer que los mismos se ubicaran justo uno al lado del otro aplicando la flotación en los tres elementos así:

```css
float: left;
```

Y nuestro resultado sería el siguiente:

![alt text](./images/img17.jpg 'posicionamiento flotante')

Ahora bien, ¿qué sucedería si a alguna de las 3 cajas aplicaramos `float: right;`? Veamos:

![alt text](./images/img18.jpg 'posicionamiento flotante')

Como vemos, en ese escenario la caja se ubica al costado lateral derecho de su elemento contenedor. ¿Sencillo no te parece?

Sin embargo, uno de los pequeños conflictos que trae consigo la flotación es que **cualquier elemento que se encuentre por debajo de un elemento flotante, asume que el flotante NO EXISTE**. Veamos:

![alt text](./images/img19.jpg 'posicionamiento flotante')

Como vemos, el resultado no es el que esperábamos pues la caja debajo de los elementos flotados, se ubicó por detrás de los mismos y obtenemos un solapamiento de cajas. ¿Qué podemos hacer entonces? ¿Cómo podemos solucionar esto?.

Por suerte, CSS nos da otra popiedad llamada `clear`, la cual recibe el valor `both` que debe ser aplicada **EN EL ELEMENTO QUE NO FLOTA** para que el mismo, se ubique por debajo de los flotados. Veamos:

![alt text](./images/img20.jpg 'posicionamiento flotante')

Como vemos, el `clear` es muy importante si queremos que aquellos elementos que *NO FLOTAN* queden por debajo de aquellos que si lo hacen, para mantener el flujo habitual de nuestro layout.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="rel"></a>
#### relative

Este tipo de posicionamiento, nos permite desplazar un elemento desde su posición original a una nueva posición. Dicho posicionamiento se logra con la propiedad `position` y el valor `relative`. Una de las características de este tipo de posicionamiento es que cuandoe es aplicado a un elemento, cualquier otro elemento que se encuentre por debajo de éste no se ve afectado. Veamos un ejemplo:

![alt text](./images/img21.jpg 'posicionamiento relativo')

En la imagen anterior vemos lo que sucedería si a la caja 1 le aplicamos `position: relative;`. La línea punteada de color rojo, es una guía de la ubicación original de la caja y una muestra de lo que le sucede con los elementos que se encuentran debajo del elemento posicionado relativamente.

Otra parte de código que podemos ver en la imagen, son dos propiedades nuevas: `top` y `left`, las mismas hacen parte de 4 propiedades en total (`right` y `bottom` son las otras dos) que suelen usarse para poder desplazar los elementos.

En este ejemplo puntal, y en cualquier escenario donde se aplique el `position: relative`. Cuando aplicamos un valor en alguna de estas propiedades, se toma como referencia el mismo costado del elemento y desde éste se dezplaza al mismo la cantidad de `px` aplicada.

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="abs"></a>
#### absolute

Con el posicionamiento absoluto, vamos a poder desplazar un elemento desde su ubicación original, hacia una nueva ubicación pero en este caso tomando como referente de movimiento los **costados del body**. Veamos un ejemplo:

![alt text](./images/img22.jpg 'posicionamiento absoluto')

Como lo podemos ver, la caja posicionada absolutamente, ahora busca el costado `right` y `bottom` del body y desde ahí se desplaza la cantidad indicada. Algo **importante** a tener en cuenta es que por más que la caja se encuentre dentro de un contenedor, la misma siempre buscará los costados del body a no se que su padre contenedor posea `position: relative`. Veamos:

> contenedor sin `position: relative;`

![alt text](./images/img23.jpg 'posicionamiento absoluto')

> contenedor con `position: relative;`

![alt text](./images/img24.jpg 'posicionamiento absoluto')

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="fix"></a>
#### fixed

El posicionamiento relativo, es muy similar al posicioamiento absoluto pero con la particularidad de que tal como su nombre lo indica, donde sea que quede el elemento el mismo va a quedar *fijo* / *pegado* indistintamente que hagamos o no scroll.

![alt text](./images/img25.gif 'posicionamiento fijo')

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

---

**Made with ❤️ by: [Javi Herrera](https://javier-herrera.com)**

*Si te parece interesante este tipo de contenido, puedes agradecerme con un Follow en mis siguientes redes sociales. Lo estimaría un montón.*

[![icon linkedin](../images/icon-linkedin.png)](https://www.linkedin.com/in/japsolo/)
[![icon instagram](../images/icon-instagram.png)](https://www.instagram.com/thefullstackdevs/)
[![icon spotify](../images/icon-spotify.png)](https://open.spotify.com/show/3J2dLuBSfzt9VVnEF8q18a)