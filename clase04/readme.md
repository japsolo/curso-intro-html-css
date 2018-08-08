# Clase IV - Selectores avanzados, Modelo de cajas y Posicionamiento 
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
  + [display: inline - inline-block - block - none](#dis)
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