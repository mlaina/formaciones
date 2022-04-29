
# HTML

**HyperText Markup Language**, es un lenguaje de marcado para definir la estructura del Document Object Model o DOM, de una página web.

Es un estándar a cargo de W3C.

HTML forma parte de un subconjunto de XML.

Entre las organizaciones oficiales donde se puede ver una definición del estándar son:

- <https://whatwg.org/>
- <https://www.w3.org/>
- <https://www.ecma-international.org/publications-and-standards/standards/>

## Editores

- **Atom**: Atom usa una licencia de software libre para su paquete y es mantenida por la comunidad de GitHub. Es sencillo de modificar, presume de ser el editor de texto más hackeable del siglo XXI.
- **Note Pad ++**: Notepad++ es un editor que fue desarrollado para máquinas basadas en Windows. Destaca por su simplicidad, además es súper liviano.
- **Sublime Text**: Sublime es uno de los mejores editores, ofrece muy buen soporte para garantizar que el programa se actualice constantemente. Los usuarios pueden agregar plugins creados por la comunidad o crear los suyos propios. Es de una empresa Australiana, es freemium.
- **Visual Studio**: Esta herramienta multi-código gratuita de edición HTML viene lista para usarse con una gran variedad de funciones personalizables. Se destaca por su autocompletado y otras respuestas sintácticas inteligentes. Visual Studio Code es un programa de múltiples idiomas y plataformas. Su entorno de desarrollo trabaja mano a mano con HTML, Python y otros lenguajes de programación populares. Microsoft.

## Inspeccionar Elemento

Podemos ver directamente el árbol DOM de la página en la que estamos, podemos seleccionar cada elemento y obtener información muy útil de cada uno.

Al seleccionar un elemento podemos ver los estilos que afectan a ese elemento concreto. Esta herramienta es muy útil y permite que comprobemos paddings, margins, borders, tamaños con facilidad. Y que apliquemos en caliente ciertos estilos que se aplicaran instantaneamente a la página.

También podemos modificar el DOM, editarlo, copiar, cortar y pegar elementos.

Podemos con la opción de seleccionar elemento, clickar en un elemento de la página y que nos relacione con su código en html y por lo tanto con sus estilos afectados.

También podemos ver cómo computa ese elemento el navegador tras procesar los estilos.

Las propiedades, que son muy interesantes para comprender los distintos elementos y cómo van a verse afectados por el css. O puede resultarnos util al utilizar las APIs de Javascript del navegador.

Podemos utilizar la herramienta de responsive para simular distintos dispositivos y ver cómo se comportaría nuestra pagina con ese width y height.

---

HTML5 aporta ciertos avances muy interesantes sobre el HTML tradicional.

De HTML debemos saber que todas las etiquetas (o componentes), se deben cerrar
adecuadamente, algunas de las etiquetas son autoconclusivas.
Si bien es válido en HTML: </br> nosotros siempre que queramos utilizar etiquetas
autoconclusivas lo haremos de esta manera: <br/> ya que sino ECMASCRIPT no es capaz
de interpretarlo adecuadamente (ya profundizaremos en esto).
Es importante tener en cuenta que <div> la etiqueta utilizada para definir divisiones, es la
etiqueta más común (y probablemente la mayor parte de nuestros componentes se
transforman finalmente en muchos divs), sin embargo debería ser utilizado como último
recurso en nuestro código, debemos intentar sustituir estos divs por componentes más
autodescriptivos siempre que sea posible.

Se han establecido nuevos elementos que se introducen en HTML5 y cuya función es darle al navegador una pista de como realizar la separeción de elementos.

Vamos a revisar rápidamente estos elementos.

`main` - nos indica cual es el contenido más importante y principal de la página.

`article` - resalta dentro de **main** aquello que tiene más importancia.

`aside` - resalta contenido que está indirectamente relacionado con el contenido principal.

`section` - lo usamos para agrupar elementos que están relacionados.

`header` - es la sección de la parte superior de la página.

`footer` - es la sección de la parte inferior de la página.

`nav`- suele estar en los laterales o en la parte superior de la página, en esta sección hará referencia a los elementos de navegación en los que habrá links que nos redirigiran a otras zonas del sitio web.

Cómo podéis comprobar ninguno de estas etiquetas son imprescindibles, y cualquiera de ellas podría sustituirse por un simple `div`, son elementos nominativos.

Sin embargo, a la hora de programar es importante que hagamos uso de estas nuevas etiquetas ya que aportaran más claridad a la hora de programar, lo hacemos más legible y mantenible. Y algunas secciones ayudan a los motores de búsqueda a indexar la información de la página web, para establecer una relación con las palabras clave que hay en las secciones de **main/article/aside**.

Bueno, una nota antes de continuar en HTML los espacios, tabulaciones y saltos de linea no son respetados a no ser que se utilice especificamente la etiqueta `<pre>`.

También recordar que `head` no se renderiza, head contiene información muy importante de la página, pero forma parte de la pagina. Solo se reenderizará `body`.

En head podemos encontrar importación de estilos, definición de estilos, el título de la pestaña, el icono de la pestaña del navegador, e información sobre el metadata de nuestro html (cómo por ejemplo la codificación en utf-8).

## Elementos comunes, repaso

<https://www.w3schools.com/tags/ref_byfunc.asp>

## Quiz

<https://courses.w3schools.com/browse/certifications/courses/front-end-certification-exam>

## FORM *

## CSS

<http://www.csszengarden.com/>

CSS utiliza score-case.
En CSS los elementos tienen la siguiente estructura:

```css
selector {
    propertyname: value;
}
```

Los selectores pueden ser de tres tipos:

- **Tags**: son etiquetas como puede ser `div`, `nav`, `p`, etc. No se pone ninguna sintaxis especial.

```css
nav {
    color: #44444; //color RGB
}
```

- **Clases**: se establece para elementos que esten relacionados normalmente, y se les da un nombre concreto. Para usar este selector en css se utiliza `.`

```css
.myclass {
    color: #44444; /*color RGB*/
}
```

```html
<div class='myclass'>...</div>
```

- **ID**: se establece para elementos concretos y únicos. Para usar este selector en css se utiliza `#`.

```css
#myid {
    color: #44444; /*color RGB*/
}
```

```html
<div id='myid'>...</div>
```

Imaginemos que tenemos el siguiente bloque HTML, y el el siguiente bloque CSS.

¿Qué estilo se aplicaría?

```html
<div id='myid' class='myclass'>...</div>

<div class='myclass'>...</div>

<div>...</div>
```

```css
div {
    color: blue;
}

.myclass {
    color: red;
}

#myid {
    color: green;
}
```

Se aplicaría el más especifico, en este caso #myid.

El orden de prioridad es **id > class > tag**.

```html
<div style='color: pink;'>...</div>
```

Esto tiene aún más prioridad **atribute style > id > class > tag**. Es así en todos los navegadores.

La palabra clave !important se salta estos criterios de prioridad, y prioriza por encima de estas normas a su estilo. Por ejmplo:

<https://www.w3schools.com/css/tryit.asp?filename=trycss_important>

Se pueden definir estilos específicos para hijos cuyos padres sean otro selector. Por
ejemplo:

```css
div > p {
    background-color: yellow;
}
```

Selecciona y aplica estilo a cada elemento `<p>` donde el padre inmediato sea un elemento
`<div>`.

```css
div p {
    background-color: yellow;
}
```

Selecciona y aplica estilo a cada elemento `<p>` que tenga en el DOM un elemento por
encima que sea `<div>`.

La conjunción de estos selectores son más específicos, y tienen más prioridad, que sus
equivalentes individuales.

### Tricks

<https://css-tricks.com/>

### Grid *

<https://developer.mozilla.org/es/docs/Web/CSS/CSS_Grid_Layout>
