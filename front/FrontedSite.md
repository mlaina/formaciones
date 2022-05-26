# Frontend Site

## Temática

Vamos a relizar una práctica por equipos. Vamos a realizar el desarrollo de un sitio web que vendrá definido por una de las temáticas relacionadas con las siguientes APIs de las que consumiremos sus datos:

- [Frutas](https://www.fruityvice.com/) -> we-love-mangos
- [Perros](https://thedogapi.com/) -> we-love-huskies
- [Harry Potter](https://wizard-world-api.herokuapp.com/swagger/index.html) -> we-love-doby
- [Game of Thrones](https://thronesapi.com/) -> we-hate-bran
- [Star Wars](https://swapi.dev/) -> we-hate-new-triology
- [Twitter](https://developer.twitter.com/en/docs) -> we-love-trends
- [Spotify](https://developer.spotify.com/documentation/web-api/) -> we-love-acdc
- [Tripadvisor](https://www.tripadvisor.com/developers) -> we-hate-benidorm
- [Nasa](https://api.nasa.gov/) -> we-love-ovnis
- [The New York Times](https://developer.nytimes.com/) -> we-love-news
- [FBI](https://www.fbi.gov/wanted/api) -> we-love-detectives

El nombre del equipo vendrá definido por la API que elijan.
Subiremos nuestro código a un repositorio público en github.

---

## Recomendaciones

### Diseño

Se recomienda usar alguna herramienta de mockup de diseño para establecer cómo se va a realizar la implementación de las pantallas.

- <https://whimsical.com/>
- <https://www.figma.com/>
- <https://miro.com/>

### Repositorio

Crearemos un repositorio público en github, en una organización, cuyo nombre viene definido por la api que habéis elegido. Tendremos que configurar bien el repositorio tal y como se indica en <https://pages.github.com/>

### Entorno

Una vez creado el repositorio, haremos un `git clone` y prepararemos nuestro proyecto y entorno:

- Debemos tener Node instalado si queremos utilizar NPM pero no es obligatorio, se pueden utilizar cualquier servidor simples. Pero los archivos JS tienen que estar modulados.

- Nuestro proyecto debe tener un index.html desde el que se importarán CSS y Javascript.

- Podéis usar el editor que queráis, os recomiendo:
<https://code.visualstudio.com/>

### Implementación

Cualquier duda escribirme a Slack por privado y me meto allí donde estéis trabajando.
La implementación biene fuertemente marcada por los requisitos, leerlos todos antes de comenzar.

---

## Requisitos

No se permite hacer uso de frameworks ni librerías, solo HTML, CSS, JS y un servidor simple, que podemos usar con NPM, python o lo que queramos.

- **Primera página:** Vamos a realizar un **Grid**. En este Grid vamos a integrar alguna imagen, pondremos una pequeña descripción sobre la temática del sitio, habrá una sección para la animación que ahora comentaremos, habrá una sección para presentar a los integrantes del equipo.

- **Primera página:** Tiene que haber una **animación CSS** con keyframes, no tiene por qué ser muy elaborada pero si que quiero que jugéis un poco con los keyframes. Al cargar esa página o al pulsar un botón se debe ejecutar la animación.

- Al menos **3 páginas distintas** (rutas dentro de nuestro sitio), esto implica una manera de navegar por la aplicación de forma fluida y poder volver a Home de manera rápida.

- **Segunda página:** Haremos una llamada a una de las **APIs** propuestas, de la que tendremos que obtener una lista de elementos, los cuales mostraremos, con un diseño accesible e interesante para el usuario.

- **Tercera página:** Modificaremos con javascript los elementos del árbol del DOM, añadiendo distintos divs de distintos colores. Esta página es un **lienzo en blanco** en la que debéis sacar vuestra vena creativa, podéis poner botones que modifiquen la visualización de la página o jugar con la posición del puntero... ¡Lo que se os ocurra!

Los JS tienen que estar en módulos. Bien divididos por funcionalidades o páginas.
