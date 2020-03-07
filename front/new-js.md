# JS - ECMAScript6

Contenido:
  - [**Modules**](#modules)
  - [**Let and Const**](#let-and-const)
  - [**Literales de objetos mejorados**](#literales-de-objetos-mejorados)
  - [**Parametros por defecto**](#parametros-por-defecto)
  - [**Templates Strings**](#templates-strings)
  - [**Classes**](#classes)
  - [**Funciones con flecha**](#funciones-con-flecha)
  - [**Promesas**](#promesas)
  - [**Desestructuración**](#desestructuraci%c3%b3n)
  - [**Operador extendido**](#operador-extendido)



## **Modules**
Un script es un módulo.

Los módulos pueden cargarse entre sí y usar directivas especiales de exportación e importación para intercambiar funcionalidades, llamar a funciones de un módulo desde otro:

- `export`: exporta variables y funciones de etiquetas de palabras clave a las que se debe poder acceder desde fuera del módulo actual.

~~~
// 📁 sayHi.js
export function sayHi(user) {
  alert(`Hello, ${user}!`);
}
~~~

- `import`: permite importar funcionalidades desde otros módulos.

~~~
// 📁 main.js
import {sayHi} from './sayHi.js';

alert(sayHi); // function...
sayHi('John'); // Hello, John!
~~~

## **Let and Const**
- **var**: El alcance de una variable definida con la palabra clave “var” se limita a la funcitión dentro del cual se define. Si se define fuera de cualquier función, el alcance de la variable es global.
**var is “function scoped” (alcance).**

- **let**: El alcance de una variable definida con la palabra clave “let” o “const” se limita al bloquedefinido por llaves i.e. {} .
**“let” y “const” son “block scoped”.**

- **const**: El alcance de una variable definida con la palabra clave “const” está limitado al bloque definido por llaves. Sin embargo, si una variable se define con la palabra clave const, no se puede reasignar.
**“const” no se puede reasignar a un nuevo valor. Sin embargo, PUEDE ser mutado.**

## **Literales de objetos mejorados**

Las propiedades de los objetos a menudo se crean a partir de variables con el mismo nombre. Por ejemplo:

~~~
// ES5 code
var
  a = 1, b = 2, c = 3;
  obj = {
    a: a,
    b: b,
    c: c
  };

// obj.a = 1, obj.b = 2, obj.c = 3
~~~
No hay necesidad de repeticiones en ES6...

~~~
// ES6 code
const lib = (() => {

  function sum(a, b)  { return a + b; }
  function mult(a, b) { return a * b; }

  return {
    sum,
    mult
  };

}());

console.log( lib.sum(2, 3) );  // 5
console.log( lib.mult(2, 3) ); // 6
~~~

~~~
// lib.js
function sum(a, b)  { return a + b; }
function mult(a, b) { return a * b; }

export { sum, mult };
~~~

## **Parametros por defecto**

El parámetro predeterminado es una forma de establecer valores predeterminados para los parámetros de función en los que no se pasa un valor (es decir, no está definido).

~~~
function greet(name = "noob master") {
  console.log("Welcome mr." + name);
}
  
greet("Jagathish"); // Welcome mr.Jagathish
greet(); //Welcome mr.noob master
greet(""); //Welcome mr.
~~~

## **Templates Strings**

Las plantillas de cadena de texto (template strings) son literales de texto que habilitan el uso de expresiones incrustadas. Es posible utilizar cadenas de texto de más de una línea, y funcionalidades de interpolación de cadenas de texto con ellas.

~~~
`cadena de texto`

`línea 1 de la cadena de texto
 línea 2 de la cadena de texto`

`cadena de texto ${expresión} texto`

tag `cadena de texto ${expresión} texto`
~~~

Los caracteres de fin de línea encontrados son parte de la plantilla de cadena de texto. En el caso de cadenas de texto normales, esta es la sintaxis necesaria para obtener cadenas de más de una línea:

~~~
//ES5
console.log("línea 1 de cadena de texto\n\ línea 2 de cadena de texto");
// "línea 1 de cadena de texto
// línea 2 de cadena de texto"

//ES6
// Para obtener el mismo efecto con cadenas de texto multilínea, con ES6 es posible escribir:
console.log(`línea 1 de la cadena de texto 
línea 2 de la cadena de texto`);
// "línea 1 de la cadena de texto
// línea 2 de la cadena de texto"
~~~

## **Classes**

Con las clases javascript también tiene capacidad de ser un lenguaje orientado a objetos con herencia y todo lo que eso conlleva.

~~~
const person = new Person('John', 'Smith');
class Person{
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}
~~~

También podemos definir una clase por una expresión de clase, que es una sintaxis alternativa. Pueden ser con o sin nombre. También podemos asignar una clase a una variable como lo hacemos con las funciones. Si hacemos eso, podemos hacer referencia a la clase por su nombre. Por ejemplo, podemos definir:

~~~
let Person = class {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}
~~~~

Luego, para obtener el nombre de la clase, podemos usar la propiedad `name`. Entonces si escribimos:

~~~
console.log(Person.name)
~~~

~~~
class Person{
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  get fullName(){
    return `${this.firstName} ${this.lastName}`  
  }
  sayHi(){
    return `Hi, ${this.firstName} ${this.lastName}`
  }
}
~~~

## **Funciones con flecha**

La expresión de función flecha tiene una sintaxis más corta que una expresión de función convencional y no vincula sus propios this, arguments, super, o new.target. Las funciones flecha siempre son anónimas. Estas funciones son funciones no relacionadas con métodos y no pueden ser usadas como constructores.

~~~
const materials = [
  'Hydrogen',
  'Helium',
  'Lithium',
  'Beryllium'
];

console.log(materials.map(material => material.length));
// expected output: Array [8, 6, 7, 9]
~~~

~~~
(param1, param2, …, paramN) => { sentencias }
(param1, param2, …, paramN) => expresion
// Equivalente a: () => { return expresion; } 

// Los paréntesis son opcionales cuando sólo dispone de un argumento: singleParam => { statements } 
(singleParam) => { sentencias } singleParam => { sentencias }

// Una función sin argumentos requiere paréntesis: 
() => { sentencias }
~~~

## **Promesas**

Una `Promise` (promesa en castellano) es un objeto que representa la terminación o el fracaso eventual de una operación asíncrona. Dado que la mayoría de las personas consumen promises ya creadas, esta guía explicará primero cómo consumirlas, y luego  cómo crearlas.

Esencialmente, una promesa es un objeto devuelto al cuál se adjuntan funciones `callback`, en lugar de pasar callbacks a una función.

~~~
const promesa = crearArchivoAudioAsync(audioConfig);
promise.then(exitoCallback, falloCallback);
~~~

~~~
hazAlgo()
.then(resultado => hazAlgoMas(resultado))
.then(nuevoResultado => hazLaTerceraCosa(nuevoResultado))
.then(resultadoFinal => {
  console.log(`Obtenido el resultado final: ${resultadoFinal}`);
})
.catch(falloCallback);
~~~

## **Desestructuración**

La sintaxis de asignación de desestructuración (destructuring assignment) es una expresión que posibilita la extracción de datos, tanto de arreglos como de propiedades de objetos, en variables distintas.

~~~
let a, b, rest;
[a, b] = [10, 20];
console.log(a); // 10
console.log(b); // 20

[a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]

({ a, b } = { a: 10, b: 20 });
console.log(a); // 10
console.log(b); // 20


// Propuesta de etapa 4 (terminada)
({a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40});
console.log(a); // 10
console.log(b); // 20
console.log(rest); // {c: 30, d: 40}
~~~

~~~
const foo = ['uno', 'dos', 'tres'];

const [rojo, amarillo, verde] = foo;
console.log(rojo); // "uno"
console.log(amarillo); // "dos"
console.log(verde); // "tres"

let a, b;

[a=5, b=7] = [1];
console.log(a); // 1
console.log(b); // 7

let key = "z";
let { [key]: foo } = { z: "bar" };

console.log(foo); // "bar"
~~~

## **Operador extendido**

La sintaxis extendida o spread sintax permite a un elemento iterable tal como un arreglo o cadena ser expandido en lugares donde cero o más argumentos (para llamadas de  función) ó elementos (para Array literales) son esperados, o a un objeto ser expandido en lugares donde cero o más pares de valores clave (para literales Tipo Objeto) son esperados.

~~~
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

console.log(sum(...numbers));
// expected output: 6

console.log(sum.apply(null, numbers));
// expected output: 6
~~~