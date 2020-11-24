---
id: ecmascript
title: ECMAScript 2015+
sidebar_label: ECMAScript
---
> Guter Überblick zu ECMAScript 2015: http://es6-features.org/

## Constants and Scoping

Mit ```let``` (und auch ```const```) deklarierte Variablen sind in
JavaScript in der Sichtbarkeit eingeschränkt auf den definierenden
Block (**lexical Scope**), nicht mehr die Funktion bzw. den globalen
Context. Das gilt auch für innere Funktionen.

## Fat-Arrow

Neue Syntax zur Definition von Funktionen:

```typescript title="statement body"
  const fn = (a,msg) => { console.log(msg, a); };
```

```typescript title="expression body"
  const fn = (a,b) => a + b;
```

Die runden Klammern um die Parameter können bei genau einem Parameter wegfallen.
Im Funktionsrumpf ist das ```this``` lexikalisch gebunden an den äußeren Scope.

## Template Strings

Mit *backtics `* eingeschlossene Strings können mehrzeilig sein. Über
```${expr}``` können Ausdrücke interpoliert werden.

```typescript
  const preis = 3.99;
  const msg = `
    <div>
      Preis: ${preis}
    </div>
  `;
```

## Rest- und Spread-Operator

Der Rest-Operator (```...args```) wird vor Funktions-Parametern eingesetzt. Er
*sammelt* alle weiteren Argumente ein. In Expressions in einem Listen-Kontext
heißt er Spread-Operator und verteilt *aufzählbare* Ausdrücke auf Listen-Elemente.

```typescript
  const zahlen = [2, 3, 5];
  const primzahlen = [...zahlen, 7, 11];
  function sum(...args) { return args.reduce( (sum, v) => sum + v); }
```

Seit ECMAScript 2018 kann der Spread-Operator auch auf Objekte angewendet werden:

```typescript
  const person = { firstname: 'Max', lastname: 'Merkel' };
  const customer = { id: 17, ...person };
```

## Default-Argumente

Funktions-Parameter können **Default**-Werte erhalten:

```typescript
  function fn(arg1, arg2 = 10) { console.log(arg1, arg2); }
```

## Object-Properties Syntax-Sugar

* Property Shorthand

```typescript
  const firstname = 'Max';
  const lastname = 'Merkel';
  const person = { firstname, lastname };
```

* Method Properties

```typescript
  const obj = {
    value: 18,
    method() { console.log(`Method, Value: ${this.value}`); }
  }
```

## Destructuring

Verteilung von Objekt-Properties (oder Array-Elementen) auf Variablen:

```typescript
  const person = { id: 17, firstname: 'Max', lastname: 'Merkel' };
  const { firstname, lastname } = person;

  // Destructuring function parameter
  function printPerson({ firstname, lastname }) {
    console.log(`${lastname}, ${firstname}`);
  }
  printPerson(person);
```
## Modules

JavaScript-Codedateien werden zu Modulen durch das Exportieren von Definitionen.
Es wird unterschieden zwischen dem Default-Export und benannten Exports. Im
Angular-Umfeld wird ausschließlich letzteres verwendet.

```typescript title="module.js"
  export const minAge = 18;
  export function add(a,b) { return a + b; };
  export class Sample {}
  export default class DefaultDemo {}
```

Der Import geschieht über das Keyword ```import```:

```typescript title="app.js"
  import DefaultExport, { minAge, add, Sample as NamedExport } from './module.js';
  // Default-Import explizit
  import default as DefaultSample from './module.js';
```

## Classes

ECMAScript 2015 bringt viel syntaktischen Zucker für Klassen-Definitionen mit.
Unter der Haube bleibt alles beim alten incl. der prototypischen Vererbung.

```typescript
  class Person {

    constructor(fname, lname) {
      this.firstname = fname;
      this.lastname = lname;
      this.id = -1;
    }

    get fullname() { return `${this.firstname} ${this.lastname}`; }

    toJson() {
      return JSON.stringify({ id: this.id, fullname: this.fullname });
    }
  }

  class Customer extends Person {

    constructor(fname, lname, email) {
      super(fname, lname);
      this.email = email;
    }

    get fullname() { return super.fullname + `(${this.email})`; }
  }
```
## For-Of Loops

Für Iterables (Arrays, ...) wird eine kompakte Syntax eingeführt:

```typescript
  const zahlen = [1,2,3,4];
  for( const z of zahlen ) {
    console.log(z);
  }
```

## Promises

Mit der Promise-Spezifikation wird eine neue API eingeführt, die bisherige
Callback-Techniken bei der Programmierung von asynchronen Funktionen ablöst.

Siehe dazu den [MDN-Artikel](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

```typescript
  // Bisher
  function asyncDemo(a, b, cb) {
    setTimeout(() => {
      cb(a+b);
    }, 1000);
  }

  // Neu
  function asyncDemo(a,b) {
    return new Promise((resolv, reject) => {
      setTimeout(() => {
        resolv(a+b);
      }, 1000);
    });
  }

  asyncDemo(17,4).then(result => {
    console.log(result);
  });
```

## async/await - Semantik

Zugeschnitten auf die Promises wurde die Programmierung mit asynchronen
Funktionen durch zwei neue Schlüsselwörter weiter vereinfacht:

```typescript
  async demo() {
    const result = await asyncDemo(17,4);
    console.log(result);
  }
```
