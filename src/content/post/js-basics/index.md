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

## ES6: import modules e type="module"

i moduli non sono nient'altro che file js con però il contesto del file isolato dal resto

```html
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Demo ES6</title>
</head>

<script type="module" src="utility.js"></script>
<script type="module" src="main.js"></script>

<body></body>
</html>
```

```js title="utility.js"
export const a = 1;

export const add = (a, b) => {
  return a + b;
};

export const divide = function (a, b) {
  return a / b;
};
```

```js title="main.js"
import { a as newA, add } from './utility.js';

console.log(add(newA, 2))
```

## import default

```js title="main.js"
import Panel, { Component } from './utility.js';

const p = new Panel()
```

```js title="utility.js"
export default class MyComponent { // posso avere solo 1 default per modulo
  constructor() {
    console.log(123)
  }
}

export function Component (a, b) => a + b;
```

## Promises

http://callbackhell.com

Le promise ci permettono di risolvere il problema delle callback hell semplificando il codice. Le promise sono un intermediario tra la parte sincrona ed asincrona del nostro codice. Una promise può essere vista come un contenitore non dipendente dal tempo, si possono impostare in modo asincrono degli osservatori che tengono d'occhio il contenitore i quali riceveranno un valore appena disponibile.

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => resolve(5), 3000);
});

p.then(
    () => new Promise((resolve, reject) => {
        setTimeout(() => resolve(50), 3000);
    })
).then(
    data => console.log(data)
).catch(
    err => console.log(err)
);
```
> async await snelliscono la sintassi e spesso sono preferibili

## Typescript: cos'è

typescript è un superset di js permette di tipizzare il codice, ad esempio creando una variabile String non potremo assegnargli un valore intero. Ha uno **static type system**, ovvero già in fase di compilazione verifica se il tipo di dato è conforme al tipo della variabile

## Inferenza in typescript

L'inferenza (in typescript come in altri linguaggi come dart) è la capacità di generare un tipo di una variabile partendo da un valore iniziale.

```ts
let a = 125;

a = 'pippo'; // errore di compilazione

// mai fare così
let b; // non do un tipo a b, sarebbe un any
// any va evitato il prima possibile

// fare una tipizzazione esplicita
let b: string;
```

## Tipizzare oggetti usando interface e gestione proprietà opzionali

```ts
interface User {
  id: number;
  name: string;
  surname?: string; // proprietà opzionale
  list: string[]; // array di stringhe
  array: Array<string>; // stesso risultato usando le generics
}

let user: User; // Inizializzo una variabile di tipo User
```

## Utilizzo di class e type per la tipizzazione

Ci sono altre 2 possibilità per definire un tipo di dato:
### class

```ts
class User {
  constructor(private id: number, public name: string) {}
}
```

### type

```ts
type User = {
  id: number;
  name: string;
}

type Role = 'admin' | 'guest'; // Union types
```

Quando usare uno o l'altro? Quando possibile usare le interface, anche perchè in fase di compilazione non pesano niente. Le classi hanno il vantaggio di poter essere usate con il paradigma ad oggetti (posso fare new Class) ma ogni istanza occuperà più memoria e le classi, convertite in funzioni occuperanno comunque di più.

type invece può essere utile per combinare diversi tipi di dato insieme come union intersections ecc.

## getter & setter

```ts
get getId() {
  return this.id;
}

set setId(newId: number) {
  this.id = newId;
}

console.log(getId);
setId = 123;
```

Molto spesso si tende ad evitare setter e getter in favore di public per avere un codice più coinciso e leggibile. (ma la soluzione più indicata sarebbero i getter & setter).