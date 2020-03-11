# **React - Redux**

[Cory House](https://hackernoon.com/@housecor)

**Redux** se encarga del control de estados (sesión?) del frontal, en este caso react.

Javascript moderno (ver apuntes de [new-js.md](./new-js.md)).

Plugin para **Visual Studio Code** [**ES7 React/Redux/GraphQL/React-Native snippets**](https://marketplace.visualstudio.com/itemdetails?itemName=dsznajder.es7-react-js-snippets) 

 Why **Redux**?
 - Un Store
 - Repetimiento reducido
 - Isomorphia / Amigable
 - Inmutable Store
 - Recarga en caliente
 - Time-travel debugging
 - Es ligero 


---
## Entorno

Construcción de nuestro propio development environment:
- Node
- Webpack
- Babel
- ESLint
- npm scripts


Pasos
- Install node
- Download visual studio code
- `npm install --global prettier`
- Configurar [prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)  format on save
- npm install
- Webpack

Creación de `webpack.config.js`.
 

---
## React components

Dos discusiones:

- **Class vs Function**

- **Container vs Presentation**


Cuatro caminos para crear componentes en react.

- createClass
~~~
var HelloWorld = React.createClass({
    render : function () {
        return (
            <h1>Hello World</h1>
        );
    }
});
~~~

- ES class
~~~
class HelloWorld extends React.Component {
    constructor(props) {
        super(props);
    }

    render() {
        return (
            <h1>Hello World</h1>
        );
    }
}
~~~

- Function

~~~
function HelloWorld(props) {
    return (
        <h1>Hello World</h1>
    );
}
~~~

- Arrow function
~~~
const HelloWorld = (props) => <h1>Hello World</h1>
~~~


Si necesita un estado en su componente, deberá crear un componente de clase o elevar el estado al componente principal y pasarlo al componente funcional mediante accesorios.

Entonces, ¿por qué debería usar componentes funcionales?
Puede preguntarse por qué debería usar componentes funcionales, si eliminan tantas características agradables. Pero hay algunos beneficios que obtienes al usar componentes funcionales en React:

- Los componentes funcionales son mucho más fáciles de leer y probar porque son funciones simples de JavaScript sin estado o ganchos de ciclo de vida
- Terminas con menos código
- Te ayudan a usar las mejores prácticas . Será más fácil separar el contenedor y los componentes de presentación porque necesita pensar más sobre el estado de su componente si no tiene acceso a setState () en su componente
- El equipo de React mencionó que puede haber un aumento de rendimiento para el componente funcional en futuras versiones de React



Debe usar componentes funcionales si está escribiendo un componente de presentación que no tiene su propio estado o necesita acceder a un enlace de ciclo de vida. De lo contrario, puede pegarse a los componentes de clase o echar un vistazo a la biblioteca recomponer lo que le permite escribir componentes funcionales y mejorar con un estado o ciclo de vida de ganchos con hocs!



Container:
- Poco a ningún marcado
- Pasar datos y acciones hacia abajo
- Saber sobre redux
- A menudo con estado
  
Presentation:
- Casi todo el marcado
- Recibir datos y acciones a través de accesorios
- No hace falta saber sobre Redux
- A menudo no hay estado



"Cuando notas que algunos componentes no usan accesorios que reciben, sino que simplemente los envían hacia abajo ... es un buen momento para introducir algunos componentes del contenedor."

---

Create app foundation
- Create first pages
- Create layout
- Setup navigation



---
# Redux

- **Lift State**, User data, lfted to common ancestor and passed down to children. Components need user data but 6 other components must pass it down on props. Problem Prop Drilling.
- **React context**, UserContext. Provider (Holds user data and funcs). UserContext.Consumer. UserContext.Provider.
- **Redux**: Store.


~~~
Object.assign

{...myObj}

.map
~~~


~~~
Object.assign(target, ...sources);

Object.assign({}, state, {role:'admin'});

const newState = { ...state, role:'admin' };

const newUsers = [...state.users]

const user = {
    name : 'Cory',
    address: {
        state: 'California'
    }
}

const userCopy = {...user};

const userCopy = {...user, addres: {...user.address}};
~~~


**Immer**



Escribe funciones reductoras independientes pequeñas que son responsables de las actualizaciones de un segmento específico de estado. Llamamos a este patrón "composición reductora ". Todos, algunos o ninguno de ellos pueden manejar una acción determinada.


Container : 
- Centrarse en cómo funcionan las cosas
- Conciente de Redux
- Suscribirse a Redux State
- Dispatch Redux Actions

Presentational:
- Concéntrese en cómo se ven las cosas
- Inconsciente de Redux
- Leer datos de props
- Invocar callbacks on props


## A chat with Redux

- **React**: Hola CourseAction, alguien hizo clic en este botón.
- **Action**: Gracias react! Enviaré una acción para que los reductores que cuidan puedan actualizar el estado.
- **Reducer**: Ah, gracias a Action. Veo que me pasaste el estado actual y la acción a realizar. Haré una nueva copia del estado y la devolveré.
- **Store**: Gracias por actualizar el Reducer de estado. Me aseguraré de que todos los componentes conectados estén al tanto.
- **React-Redux**: gracias store. Ahora determinaré de manera inteligente si debo decirle a React sobre este cambio para que solo tenga que molestarse en actualizar la IU cuando sea necesario.
- **React**: Oooo! ¡Nuevos datos brillantes se han transmitido a través de accesorios del Store! ¡Actualizaré la interfaz de usuario para reflejar esto!