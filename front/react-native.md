# **react-native**

## **why use it?**
- Cross platform, al final del desarrollo genera una verdadera aplicación nativa (no es "web view", a diferencia de cordoba o ionic)
- El rendimiento operativo de la aplicación es similar al de las aplicaciones nativas.
- Fácil de aprender ¿?

---
## **Esencia**
**react-native** se basa en componentes.
Las propias librerías de react-native tienen multitud de componentes útiles.

`<View>`   - equivalente a un div contenedor

---
## **Instalación react-native**

Primero hay que instalarse node y npm, las últimas versiones.
- `npm i -g react-native-cli`
- `npm i -g create-react-native-app`
- `react-native init reactNativeCli`
- `create-react-native-app my-proyect`

Con **yarn**.

Con emuladores de android e iOS.

O bien generar el proyecto con **Expo**

- `npm install --global expo-cli`
- `expo init my-proyect`

Mirar **Ignite Cli**

---
## **Componentes**

Se utiliza la sintaxis de jsx **ES6**.

Todas las clases que extienden a `React.Component` tienen una función `render()` que devuelve un código que al final de todos los renderizados en cascada finaliza con el html equivalente que posteriormente se convierte a la sintexis de **Android** e **iOS**.

El estilo se comporta de manera similar a CSS, mediante la clase `StyleSheet`, a diferencia de que los atributos utilizan *CammelCase*.

~~~
import React, { Component } from 'react';
import { StyleSheet, Text, View } from 'react-native';

const styles = StyleSheet.create({
  bigBlue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

export default class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigBlue}>just bigBlue</Text>
        <Text style={[styles.bigBlue, styles.red]}>bigBlue, then red</Text>
        <Text style={[styles.red, styles.bigBlue]}>red, then bigBlue</Text>
      </View>
    );
  }
}

~~~

---
## **Expo**

Instalar la aplicación de **Expo** en tu móvil.

- `npm install -g exp`

Lo que hace expo es levantar un servicio con un protocolo  **exp** y generar un código **QR** para poder ir directamente a la **ip** del ordenador de desarrollo en el que está corriendo el servicio. De esta manera con la aplicación movil simulamos una aplicación nativa.

---
## **Debug Expo**

- `npm install -g react-devtools`
- `react-devtools`

En la app de Expo `developer menu -> debug js remotely`.

Marcar `Pause on caught exception...` se marcará lo que marcas en el DOM, en la estructura HTML.

---
## **Componente View**

Container que tiene n hijos.

Estructura del proyecto:
- App
  - View
    - Home.js
    - ..
    - ..
- App.js
- package.json

~~~
  render() {
    return (
      <Home />
    );
  }
~~~

---
## **Props State**

### Props
Parametros, son propiedades que se utilizan como parametros en el renderizado del componente

~~~
import React, { Component } from 'react';
import { Image } from 'react-native';

export default class Bananas extends Component {
  render() {
    let pic = {
      uri: 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg'
    };
    return (
      <Image source={pic} style={{width: 193, height: 110}}/>
    );
  }
}

~~~

### State
Hay dos tipos de datos que controlan un componente **props** y **state**. **Props** los establece el padre y se utilizan a lo largo de la vida del componente. Para los datos que van a cambiar se utiliza **State**.

~~~
import React, { Component } from 'react';
import { Text, View } from 'react-native';

class Blink extends Component {

  componentDidMount(){
    // Toggle the state every second
    setInterval(() => (
      this.setState(previousState => (
        { isShowingText: !previousState.isShowingText }
      ))
    ), 1000);
  }

  //state object
  state = { isShowingText: true };

  render() {
    if (!this.state.isShowingText) {
      return null;
    }

    return (
      <Text>{this.props.text}</Text>
    );
  }
}

export default class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}

~~~

--- 
## **Layout**

- **Flex dimensions**: Use flexel estilo de un componente para que el componente se expanda y se reduzca dinámicamente según el espacio disponible. Normalmente lo usará flex: 1, que le dice a un componente que llene todo el espacio disponible, compartido de manera uniforme entre otros componentes con el mismo padre. Cuanto mayor sea el valor flexdado, mayor será la proporción de espacio que ocupará un componente en comparación con sus hermanos.
Un componente sólo puede expandirse para llenar el espacio disponible si su padre tiene dimensiones mayores que 0. Si un padre no tiene ya sea un fijo widthy height, o flex, el padre tendrá unas dimensiones de 0 y los flexniños no serán visibles.
- **Flex direction**: controla la dirección en la que se disponen los elementos secundarios de un nodo. Esto también se conoce como el eje principal . El eje transversal es el eje perpendicular al eje principal, o el eje en el que se disponen las líneas de ajuste.

  - `rowAlinea` a los niños de izquierda a derecha. Si el ajuste está habilitado, la siguiente línea comenzará debajo del primer elemento a la izquierda del contenedor.

  - `column`( valor predeterminado ) Alinear hijos de arriba a abajo. Si el ajuste está activado, la siguiente línea comenzará con el primer elemento izquierdo en la parte superior del contenedor.

  - `row-reverse` Alinea a los niños de derecha a izquierda. Si el ajuste está habilitado, la siguiente línea comenzará debajo del primer elemento a la derecha del contenedor.

  - `column-reverse` Alinea a los niños de abajo hacia arriba. Si el ajuste está activado, la siguiente línea comenzará con el primer elemento izquierdo en la parte inferior del contenedor.
 
- **Justify Content**: describe cómo alinear a los niños dentro del eje principal de su contenedor. Por ejemplo, puede usar esta propiedad para centrar un elemento secundario horizontalmente dentro de un contenedor con flexDirectionset to rowo verticalmente dentro de un contenedor con flexDirectionset to column.

  - `flex-start` ( valor predeterminado ) Alinea los elementos secundarios de un contenedor al inicio del eje principal del contenedor.

  - `flex-end` Alinea los elementos secundarios de un contenedor al final del eje principal del contenedor.

  - `center` Alinea los elementos secundarios de un contenedor en el centro del eje principal del contenedor.

  - `space-between` Espacio uniforme de los niños a través del eje principal del contenedor, distribuyendo el espacio restante entre los niños.

  - `space-around` Espacio uniforme de los niños a través del eje principal del contenedor, distribuyendo el espacio restante alrededor de los niños. En comparación con el space-betweenuso space-around, el espacio se distribuirá al principio del primer hijo y al final del último hijo.

  - `space-evenly` Distribuido uniformemente dentro del contenedor de alineación a lo largo del eje principal. El espacio entre cada par de elementos adyacentes, el borde de inicio principal y el primer elemento, y el borde del extremo principal y el último elemento, son exactamente iguales.
  
- **Align Items**: describe cómo alinear a los niños a lo largo del eje transversal de su contenedor. Alinear elementos es muy similar justifyContentpero, en lugar de aplicarse al eje principal, se alignItemsaplica al eje transversal.

  - `stretch`( valor predeterminado ) Estirar los elementos secundarios de un contenedor para que coincidan con el heighteje transversal del contenedor.

  - `flex-start` Alinee los elementos secundarios de un contenedor al inicio del eje transversal del contenedor.

  - `flex-end` Alinee los elementos secundarios de un contenedor al final del eje transversal del contenedor.

  - `center` Alinea los elementos secundarios de un contenedor en el centro del eje transversal del contenedor.

  - `baseline` Alinea los elementos secundarios de un contenedor a lo largo de una línea base común. Se puede establecer que los niños individuales sean la referencia de referencia para sus padres.



~~~

{styles.container}
{{flex:6}}
{{flex:8}}


const styles = StyleSheet.create({
    container: {
        flex:1,
        flexDirection: 'row', /* ('column-reverse') */
        justifyContent: 'center',
        alignItems: 'center'
    }    
});

~~~

---
## **Platform**

Se puede hacer código específico de una plataforma, ya sea android o iOS.

~~~

import { Pltform } from 'react-native';


if(Platform.OS === 'android'){
    estas en android
}



headStyle:{
    ... Platform.select({
        ios:{
            height:300
        },
        android:{
            height:300
        }
    })

}

this.state = {
    isLoggedIn:false,
    theVersion: Platform.Version
};

~~~
Si el componente es muy específico tambien se puede definir un componente para iOS y otro para Android.

Home.ios.js
Home.android.js


---
## **Images**

http -> no está permitido en el App Store, solo https.

Mejor tener las imagenes en el proyecto en una carpeta cercana a las secciones.

- app
    - sections
        - img
            - archivo.svg
            - .
            - .
        - Header.js
    - views
        - Home.js


Utilización del componente `Image`. 

~~~

render(){
    return (
        <Image
        style={styles.image}
        source={ require('./img/archivo.svg')}
        />
    );
}

~~~

Con el estilo **flex** le damos el tamaño que requiere la imagen.

---

## **Touch**


### **Button**

Tiene un **prop** `onPress`
~~~
<Button
onPress={someMethod} />
~~~


Para hacer tus propios componentes es necesaria la utilización de los siguientes componentes implementados en `react-natavie`.

### **TouchableHighlight**

Un contenedor para hacer que las vistas respondan adecuadamente a los toques. Al presionar hacia abajo, la opacidad de la vista ajustada disminuye, lo que permite que se vea el color subyacente, oscureciendo o teñiendo la vista.

La capa subyacente proviene de envolver al niño en una nueva Vista, lo que puede afectar el diseño y, a veces, causar artefactos visuales no deseados si no se usa correctamente, por ejemplo, si el Color de fondo de la vista ajustada no se establece explícitamente en un color opaco.

TouchableHighlight debe tener un hijo (no cero o más de uno). Si desea tener varios componentes secundarios, envuélvalos en una Vista.

~~~
<TouchableHighlight onPress={this._onPressButton}>
    <Image source={require('.myButton.png')}>
</TouchableHighlight>
~~~


### **TouchableWithoutFeedback**

Un contenedor para hacer que las vistas respondan correctamente a los toques (solo Android). En Android, este componente utiliza un estado nativo que se puede dibujar para mostrar comentarios táctiles.

Por el momento, solo admite tener una única instancia de Vista como nodo secundario, ya que se implementa reemplazando esa Vista con otra instancia del nodo RCTView con algunas propiedades adicionales establecidas.

El fondo dibujable de la retroalimentación nativa que se puede tocar se puede personalizar con la backgroundpropiedad

~~~
<TouchableWithoutFeedback onPress={this._onPressButton}>
    <View>
        <Text> No Feedback </Text>
    </View>
</TouchableWithoutFeedback>
~~~


### **TouchableOpacity**

Un contenedor para hacer que las vistas respondan adecuadamente a los toques. Al presionar hacia abajo, la opacidad de la vista ajustada disminuye, atenuándola.

La opacidad se controla envolviendo los elementos secundarios en un Animated.View, que se agrega a la jerarquía de vistas. Tenga en cuenta que esto puede afectar el diseño.

~~~
<TouchableOpacity onPress={this._onPressButton}>
    <Image source={require('.myButton')}/>
</TouchableOpacity>
~~~



**Ejemplo:**

~~~
import React, { Component } from 'react'
import {
  StyleSheet,
  TouchableOpacity,
  Text,
  View,
} from 'react-native'

export default class App extends Component {
  constructor(props) {
    super(props)
    this.state = { count: 0 }
  }

  onPress = () => {
    this.setState({
      count: this.state.count+1
    })
  }

 render() {
   return (
     <View style={styles.container}>
       <TouchableOpacity
         style={styles.button}
         onPress={this.onPress}
       >
         <Text> Touch Here </Text>
       </TouchableOpacity>
       <View style={[styles.countContainer]}>
         <Text style={[styles.countText]}>
            { this.state.count !== 0 ? this.state.count: null}
          </Text>
        </View>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    paddingHorizontal: 10
  },
  button: {
    alignItems: 'center',
    backgroundColor: '#DDDDDD',
    padding: 10
  },
  countContainer: {
    alignItems: 'center',
    padding: 10
  },
  countText: {
    color: '#FF00FF'
  }
})
~~~~

---
## **React Navigation**

Requiere de otra dependencia. Para instalarla haremos:

`npm install --save react-navigation`


Ejemplo en el archivo `App.js`:

~~~
import React from 'react';
import { StackNavigator } from 'react-navigation';


const MyRoutes = StackNavigator({
        HomeRT: {
            screen: Home
        },
        ContactRT: {
            screen: Contact
        },
    },
    {
        initialRouteName: 'HomeRT'
    }

});


export default class App extends React.Component {
    render(){
        return ( <MyRoutes /> );
    }
}
~~~


Para hacer navegación al pulsar un botón hay que utilizar la función `navigate`:
~~~~
    <Button
        onPress={() => navigate('Chat')}
        title="Chat with Lucy"
    />
~~~~

Lo adecuado es definir la navegación en un componente padre. La propiedad
`navigation` se genera al inicializar el StackNavigator y es el controlador de la navegación que desciende a todos los componentes por **Props**.

---
## **User input**

Librería de `react-native` - `TextInput`.

***Recordatorio**: el estado (`this.state`) se inicializa en el constructor del componente haciendo un `super(props);` antes de la inicialización.*

La propiedad navigation tiene una funcion `goBack();`


Ejemplo TextInput:
~~~~
import React, { Component } from 'react';
import { Text, TextInput, View } from 'react-native';

export default class PizzaTranslator extends Component {
  constructor(props) {
    super(props);
    this.state = {text: ''};
  }

  render() {
    return (
      <View style={{padding: 10}}>
        <TextInput
          style={{height: 40}}
          placeholder="Type here to translate!"
          onChangeText={(text) => this.setState({text})}
          value={this.state.text}
        />
        <Text style={{padding: 10, fontSize: 42}}>
          {this.state.text.split(' ').map((word) => word && '🍕').join(' ')}
        </Text>
      </View>
    );
  }
}
~~~~

---
## **External Data**

`componentDidMount()` se invoca inmediatamente después de que un componente se monte (se inserte en el árbol). La inicialización que requiere nodos DOM debería ir aquí. Si necesita cargar datos desde un punto final remoto, este es un buen lugar para instanciar la solicitud de red.

Este método es un buen lugar para establecer cualquier suscripción. Si lo haces, no olvides darle de baja en `componentWillUnmount()`.

*La API Fetch proporciona una interfaz JavaScript para acceder y manipular partes del canal HTTP, como peticiones y respuestas. También provee un método global `fetch()` que proporciona una forma fácil y lógica de obtener recursos de forma asíncrona por la red.*

*Este tipo de funcionalidad se conseguía previamente haciendo uso de XMLHttpRequest. Fetch proporciona una mejor alternativa que puede ser empleada fácilmente por otras tecnologías como Service Workers. Fetch también aporta un único lugar lógico en el que definir otros conceptos relacionados con HTTP como CORS y extensiones para HTTP.*

Ejemplo de `fetch`:

~~~
fetch('http://example.com/movies.json')
  .then(function(response) {
    return response.json();
  })
  .then(function(myJson) {
    console.log(myJson);
  });
~~~~

Es muy útil mediante **state** utilizar estados y en los render utilizar condicionales dependientes de esos estados. Por ejemplo en caso de tener una promesa que aún no se ha cargado (como utilizando `fetch`), tener una actualización de estado cuando termine el fetch, y que mientras tanto el componente renderice un *LOADING...*

Con **WebView**  se pueden colocar iframes de otras webs. Por ejemplo la visualización de vidos de youtube se haría mediante la API de youtube y mandándole la información necesaria para la visualización del video.

---
## **User registration**

Para guardar cosas localmente es necesaria la librería **AsyncStorage** de react-native.

~~~

export class Register extends React.Component{

  constructor(props){
    super(props);
    this.state= {
      username: '',
      password: '',
      passwordConfirm: ''
    };
  };

  registerAccount = () => {
    if( !this.state.username ){
      Alert.alert("Error, enter a username");
    } else if ( this.state.password != this.state.passwordConfirm ) {
      Alert.alert("No coinciden las contraseñas")
    } else{
      AsyncStorage.getItem(this.state.username, (err, result)=>{
        if( result !== null ){
          Alert.alert("el usuario existe!");
        } else {
          AsyncStorage.setItem(this.state.username, this.state.password, (err, result) => {
            Alert.alert("registrado");
            this.props.navigation.navigate("HomeRT");
          })
        }

      });
    }

  }

}

~~~

`(err, result)=>{}` es la función callback que trata la operación de la función que la ha llamado. Es decir, obtenemos un resultado al ejecutar `getItem` hacemos la comprobación de ese resultado antes de proceder a la ejecución de la siguiente sentencia.

---
## **User Login**

~~~
loginUser = () => {
  if ( !this.state.userName ) {
    Alert.alert("Introduce un usuario");
  } else if ( !this.state.password ){
    Alert.alert("Introduce la contraesña);
  } else {
    AsyncStorage.getItem("userLoggedIn", (err, result) => {
      if ( result!=='none' ) {
        Alert.alert("Hay alguien logeeado");
        this.prop.navigation.navigate('HomeRT');
      } else {
        AsyncStorage.getItem(this.state.username, (err,result) => {
          if(result!=null){
            if(result!=this.state.password){
              Alert.alert("Password incorrecta);
            }else{
              AsyncStorage.setItem("userLoggedInt", this.state.username, (err, result) => {
                Alert.alert("Logged in);
                this.props.navigation.navigate('HomeRT');
              });
            }
          }else{
            Alert.alert("No account");
          }
        });
      }


    })
  }

}

~~~



---
## **Puntualizaciones**

Para exportar una variable cargada JSON:
~~~
export const Variable = {

}

.
.

import { Variable } from '../data/Variable.js'

~~~

Para poner condicionales en el render:

~~~
<View>
  { this.state.condition && (
      <View> ... </View>
    )
  }
</View>
~~~

Para utilizar parrafos HTML:

`npm install react-native-render-html --save`

~~~
import HTML from 'react-native-render-html';


render(){
  let items=' <p> ${this.props.id} </p>';
  return (
    <View>
      <HTML html="{items}" onLinkPress={()=>this.link()} classStyles={classStyles} tagStyles={tagStyles}/>
  );
}
~~~

---
## **Compiling React Native App**

INVESTIGAR HA CAMBIADO LA MANERA DE COMPILACIÓN REMOTA DE **EXPO**.