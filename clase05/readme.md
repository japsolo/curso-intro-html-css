# Clase V - Responsive Web Development - Mediaqueries y Frameworks

<a name="top"></a>

### Tabla de contenido

+ [Responsive Web Development](#rwd)
	+ [\<meta name="viewport">](#meta)
	+ [@media-queries](#queries)
	+ [min-width](#mnw)
	+ [max-width](#mxw)
+ [Bootstrap v3](#boot)
	+ [Introducción](#intro)
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

<a name="rwd"></a>	
#### min-width

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

<br>

<a name="rwd"></a>
#### max-width

[![alt text](./images/img-up.png "subir") volver a la tabla de contenido](#top)

---