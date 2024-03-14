---
title: "Concetti base di ES6/typescript"
description: "I miei appunti del corso di Fabio Biondi su ES6 e TS"
publishDate: "9 Mar 2024"
tags: ["js", "basics", "ts"]
---

## var vs let

let è block scoped mentre var è function scoped

```js
{
    let a = 123;
    var b = 123;
}
console.log(a); // undefined
console.log(b); // 123
```

## const: mutabilità vs immutabilità

const è block scoped come let e in più le variabili const non possono essere riassegnate. Questo non significa che una variabile const non possa mutare:

```js
const obj = { property: 123 }
obj.property = 456;
console.log(obj.property); // 456
```

## Template literals: stringhe multiline e con espressioni

Grazie a questa nuova sintassi risulta più comodo creare stringhe multiline o meno con al loro interno delle variabili.

```js
const age = 40;
const result = `hello Mario (${age})`;
console.log(result); // hello Mario (40)
```

## Short object syntax

Nel momento in cui chiave e valore di un oggetto coincidono posso omettere uno dei due:

```js
const age = 40;
const params = { age }
console.log(params); // { age: 40 }
```

## Destructuring

Serve per estrarre dagli oggetti/array dei valori o delle proprietà creando nuove variabili che conterrano tali valori.

```js
const list = [10, 20, 30, 40, 50]
const [a, b, ...rest] = list;

console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]

const user = {
  first: 'Fabio',
  last: 'Biondi',
  // preference: 'red'
}

let { first, preference: pref = 'black' } = user;

console.log(`${first} (${pref})`); // Fabio (black)
```

## Destructuring di nested props
Si può usare il destructuring anche su oggetti con diversi nodi al suo interno:

```js
const user = {
  name: 'Fabio',
  surname: 'Biondi',
  profile: {
    color: 'red',
    location: {
      lat: 15, lng: 12
    },
  }
};

const { 
  profile: {
 	location: {
      lat, lng, zoom = 5
    }
  }
} = user;

console.log(lat, lng, zoom) // 15, 12, 5
```

## Spread operator
Lo spread operator è una nuova sintassi di ES6 che permette di clonare, mergiare e modificare gli array.

```js
const data = [1, 2, 3, 4]
const list = [5, 6];
const merged = [...data, ...list, 7, 8];

console.log(merged); // [1, 2, 3, 4, 5, 6, 7, 8]
```

> Dietro le quinte tramite babel lo spread operator diventa un concat in ES5

## Object spread operator vs Object.assign

Entrambe le sintassi servono per creare un clone, anzi si può dire che lo spread operator sia zucchero sintattico per fare una Object.assign:

```js
// object.assign

const obj = {
  id: 123,
  name: 'Fabio'
}

const preferences = { color: 'red' };
                     
const merged = Object.assign({}, obj, preferences, { pet: 'dog' });

console.log(merged);

/**
OUTPUT:

{
  "id": 123,
  "name": "Fabio",
  "color": "red",
  "pet": "dog"
}
*/

// spread operator
const obj = {
  id: 123,
  name: 'Fabio'
}

const preferences = { color: 'red' };
                     
const merged = { ...obj, ...preferences, pet: 'dog' };

console.log(merged);

/**
OUTPUT:

{
  "id": 123,
  "name": "Fabio",
  "color": "red",
  "pet": "dog"
}
*/
```

## Arrow function
La sintassi delle arrow function è più compatta e da dei vantaggi a livello di `this` che vedremo più avanti:

```js
const add = (a, b) => {
  return a + b;
}
const divide = (a, b) => a / b;
const pow = a => a * a;
const greetings = () => console.log('hello')

greetings();
```

## Array: map
ES6 fornisce una nuova serie di metodi per lavorare gli array: map in particolare ci permette di creare una nuova collezione a partire da un array.

```js
const users = [
  {"id": 1, "name": "Silvia", "age": 2, "gender": "F", city: "Gorizia"},
  {"id": 2, "name": "Fabio", "age": 40, "gender": "M", city: "Trieste"},
  {"id": 3, "name": "Lorenzo", "age": 6, "gender": "M", city: "Pordenone"},
  {"id": 4, "name": "Lisa", "age": 40, "gender": "F", city: "Gorizia"}
];

const newList = users.map(user => `${user.name} (${user.age})`)
console.log(newList);

/*  output
[
  "Silvia (2)",
  "Fabio (40)",
  "Lorenzo (6)",
  "Lisa (40)"
]
*/
```

> Possiamo anche avere traccia dell'indice dell'elemento che si stà processando mettendo un secondo parametro dopo user


```js
const newList = users.map((user, index) => `${user.name} (${index})`);
```

## Array: filter
Crea un array partendo da un altro array andando a capire tramite un predicato (una funzione passata come argomento) se l'elemento deve essere presente o meno nel nuovo array.

```js
const users = [
  {"id": 1, "name": "Silvia", "age": 2, "gender": "F", city: "Gorizia"},
  {"id": 2, "name": "Fabio", "age": 40, "gender": "M", city: "Trieste"},
  {"id": 3, "name": "Lorenzo", "age": 6, "gender": "M", city: "Pordenone"},
  {"id": 4, "name": "Lisa", "age": 40, "gender": "F", city: "Gorizia"}
];


const newList = users.filter(user => user.age > 18)
                     .map(user => user.id)

console.log(newList);

/** output
[
  2,
  4
]
*/
```

## Array: find e findIndex
findIndex permette tramite una funzione di andare a recuperare l'indice di un elemento della collezione, mentre find restituisce l'oggetto.


```js
const users = [
  {"id": 1, "name": "Silvia", "age": 2, "gender": "F", city: "Gorizia"},
  {"id": 2, "name": "Fabio", "age": 40, "gender": "M", city: "Trieste"},
  {"id": 3, "name": "Lorenzo", "age": 6, "gender": "M", city: "Pordenone"},
  {"id": 4, "name": "Lisa", "age": 40, "gender": "F", city: "Gorizia"}
];

const userIndex = users.findIndex(user => user.id === 3);
console.log(userIndex) // 2
```

## Immutabilità in ES6

```js
const users = [
  {"id": 10, "name": "Silvia", "age": 2, "gender": "F", city: "Gorizia"},
  {"id": 20, "name": "Fabio", "age": 40, "gender": "M", city: "Trieste"},
  {"id": 30, "name": "Lorenzo", "age": 6, "gender": "M", city: "Pordenone"},
  {"id": 40, "name": "Lisa", "age": 40, "gender": "F", city: "Gorizia"}
];

// add
const user = { id: 50, name: 'Mario' };
let newList = [...users, user ]

// delete
const ID = 40;
newList = users.filter(u => u.id !== ID )

// edit
const updatedUser = { id: 20, name: 'Ciccio', age: 25 }
newList = users.map(u => u.id === updatedUser.id ? {...u, ...updatedUser} : u)

console.log(newList)
```

## Classi, Ereditarietà e lexical this
Il concetto di classe è stato introdotto da ES6, naturalmente con babel in transpilazione ad ES5 le classi vengono tradotte in funzioni

```js
class Pippo {
  text = 'Ciao';

  constructor() {    
    setTimeout(() => {
      console.log(this.text); // Se non avessi usato l'arrow function sarebbe stato undefined
    }, 2000)
  }

  hello(value) {
    console.log(this.text + ' ' + value);
  }
}

const p = new Pippo();
p.hello('Fabio'); // Ciao Fabio
```

> Per ovviare al problema del this nelle funzioni un'altro metodo valido è usare `.bind(this)`