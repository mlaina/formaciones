# JS advanced

Buenas tardes! hoy vamos a continuar con la formación de javascript que comenzamos hace dos semanas.

Hicimos un quiz de js básico en w3schools.

Vimos que es un lenguaje no tipado, muy orientado a funciones, multiparadigma ya que se puede utilizar programación declarativa y comentamos ue también soporta programación orientada a objetos.

Vimos como declarar variables, como declarar objetos y arrays.

https://rickandmortyapi.com/

## Dudas

Con `delete` podemos eliminar una propiedad de un objeto.

Con `new Object();` podemos crear tambien un objeto al igual que si hacemos un `{}`

```js
let obj = new Object();
obj.a = 3;

console.log(obj);

delete obj.a;

console.log(obj);
```

Vamos a comprobar la duda que nos surgió el otro día que comentó Carlos:

Primero el caso básico:

```js
let obj1 = {
    x:1,
    y:2
};

let obj2 = {...obj1};
//

console.log(obj2);
//
delete obj1.x;
//
console.log(obj1);
//
console.log(obj2);

```

Ahora vamos a probar con un objeto dentro de otro.
```js
let obj1 = {
    inner: {
        x:1,
        y:2
    }
};

let obj2 = {...obj1};
//

console.log(obj2);
//
delete obj1.inner.x;
//
console.log(obj1);
//
console.log(obj2);

```

Así que no se hace una copia en profundidad.

```js
 let a = { b: 1, c: { d:2, e: 3, f:{ g: 2}}};
 var obj = {};
 obj = JSON.parse(JSON.stringify(initalObj));

 delete a.c.d
 a
 obj
```

---
## Arrow functions

Las arrow functions es una forma de expresar una función en una alternativa compacta.

Hay diferencias y limitaciones de este tipo de funciones, sobre todo en lo referente a classes pero no vamos a entrar tan al detalle.

```js
function foo(a, b, c=1){
    return a+b+c;
}

foo(a,b);
```

Os recuerdo que los parametros de una función en javascript no tienen tipos asique deben ser respectivos en orden de escritura a la definición de la función. También recordar que se puede especificar un valor por defecto para que en caso de que ese parametro no se especifique en la llamada adquiera este valor.

Como arrow function se escribiría de esta manera:

```js
(a, b, c=1) => {
    return a+b+c;
}
```

Esta definición se quedaría en el aire, y a no ser que se lo pasemos a otra función como parámetro no tiene mucho sentido definirla así en caliente. Lo que podemos hacer es guardarla en una variable o una constante.

```js
const foo = (a, b, c=1) => {
    return a+b+c;
}
```

En caso de que nuestra función solo tenga una linea también podriamos utilizar este formato.

```js
const foo = (a, b, c=1) => a+b+c;
```

JS nos permite también crear ambitos concretos por ejemplo:

```js
{ let a = 3; }
```

Funciones anidadas:
Podríamos hacer uso en una función de otra función auxiliar que solo tiene sentido en este entorno.

```js
function sayHiBye(firstName, lastName) {

  function getFullName() {
    return firstName + " " + lastName;
  }

  alert( "Hello, " + getFullName() );
  alert( "Bye, " + getFullName() );

}
```

También podríamos hacer una función devolviese otra función, incluso que esa otra función cambiase una variable que solo se encuentra en el entorno de la primera.

```js
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
```

Pregunta:
```js
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
let counter2 = makeCounter();

alert( counter() ); // 0
alert( counter() ); // 1

alert( counter2() ); // ?
alert( counter2() ); // ?
```
0 y 1

Son dos contadores independientes.

```js
function sum(a) {

  return function(b) {
    return a + b; // takes "a" from the outer lexical environment
  };

}

alert( sum(1)(2) ); // 3
alert( sum(5)(-1) ); // 4
```

Los callbacks son funciones que se pasan como parámetros para que se ejecuten al final de otra función.

https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_win_settimeout

```js
setTimeout(() => document.getElementById("demo").innerHTML = "Happy Birthday!", 5000);
```

---
## Array methods 

Vamos a ver cómo podemos tratar arrays.

```js
let array = [1,2,3,4,5,6,7,8,9];
```

Modificación:

- delete

```js
delete array[4];
```

Pero que sucede? se queda un elemento `empty`, vacio en la posicion 4.

- push

```js
array.push(10)
```

- pop: nos devuelve el elemento extraido, por el final

```js
array.pop()
```

- shift: nos devuelve el elemento extraido, por el principio

```js
array.shift()
```

- unshift: añade elementos por el principio

```js
array.unshift(1)
```

- splice(pos, deleteCount, ...items)– en el índice pos elimina deleteCountelementos e inserta items.
- slice(start, end)– crea una nueva matriz, copia elementos desde el índice start hasta end(no inclusive) en ella.

```js
let arr = ["I", "study", "JavaScript"];

arr.splice(1, 1); // from index 1 remove 1 element

alert( arr ); // ["I", "JavaScript"]
```

```js
let arr = ["I", "study", "JavaScript", "right", "now"];

// remove 3 first elements and replace them with another
arr.splice(0, 3, "Let's", "dance");

alert( arr ) // now ["Let's", "dance", "right", "now"]
```

- concat

```js
let arr = [1, 2];

// create an array from: arr and [3,4]
alert( arr.concat([3, 4]) ); // 1,2,3,4

// create an array from: arr and [3,4] and [5,6]
alert( arr.concat([3, 4], [5, 6]) ); // 1,2,3,4,5,6

// create an array from: arr and [3,4], then add values 5 and 6
alert( arr.concat([3, 4], 5, 6) ); // 1,2,3,4,5,6
```

Iterables:

- forEach:

```js
["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
  alert(`${item} is at index ${index} in ${array}`);
});
```

- indexOf

```js
let arr = [1, 0, false];

alert( arr.indexOf(0) ); // 1
alert( arr.indexOf(false) ); // 2
alert( arr.indexOf(null) ); // -1

alert( arr.includes(1) ); // true
```

- includes

```js
const arr = [NaN];
alert( arr.indexOf(NaN) ); // -1 (should be 0, but === equality doesn't work for NaN)
alert( arr.includes(NaN) );// true (correct)
```

- find:

```js
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);

alert(user.name); // John
```

- filter

```js
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

// returns array of the first two users
let someUsers = users.filter(item => item.id < 3);

alert(someUsers.length); // 2
```

- map:

```js
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
alert(lengths); // 5,7,6
```

- sort:

```js
let arr = [ 1, 2, 15 ];

// the method reorders the content of arr
arr.sort();

alert( arr ); 

function compareNumeric(a, b) {
  if (a > b) return 1;
  if (a == b) return 0;
  if (a < b) return -1;
}

let arr = [ 1, 2, 15 ];

arr.sort(compareNumeric);

alert(arr);  // 1, 2, 15
```

- reverse:

```js
let arr = [1, 2, 3, 4, 5];
arr.reverse();

alert( arr ); // 5,4,3,2,1
```

- reduce

```js
let arr = [1, 2, 3, 4, 5];

let result = arr.reduce((sum, current) => sum + current, 0);

alert(result); // 15
```

Split string:

```js
let arr = 'Bilbo, Gandalf, Nazgul, Saruman'.split(', ', 2);

alert(arr); // Bilbo, Gandalf
```

https://javascript.info/array-methods

---

## Clases

```js
class User {

  constructor(name) {
    this.name = name;
  }

  sayHi() {
    alert(this.name);
  }

}

// Usage:
let user = new User("John");
user.sayHi();
```

Qué tipología de datos creeis que es una clase?

`typeof User`

```js
User.prototype.sayHi = function() {
  alert(this.name);
};
```

Dentro de una clase se utiliza `use strict`

Nosotros en ciertos ambitos de javascipt podemos usar el modo no estricto, por ejemplo en la consola.

Setters y getters:

```js
class User {

  constructor(name) {
    // invokes the setter
    this.name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    if (value.length < 4) {
      alert("Name is too short.");
      return;
    }
    this._name = value;
  }

}

let user = new User("John");
alert(user.name); // John

user = new User(""); // Name is too short.

```

https://www.w3schools.com/js/tryit.asp?filename=tryjs_strict_variableç

https://javascript.info/function-prototype

https://javascript.info/class

---

## Export Import

Vamos a ver cómo modularizar código en javascript:

https://javascript.info/modules-intro

https://javascript.info/import-export

https://javascript.info/modules-dynamic-imports

---

## Excepciones

https://javascript.info/try-catch

---

## Promesas

https://javascript.info/promise-basics
https://javascript.info/promise-error-handling

promise.all()

---

## fetch

https://javascript.info/fetch
https://javascript.info/promise-api

---
