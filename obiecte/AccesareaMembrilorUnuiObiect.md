## Mantre

- În obiecte numele proprietăților sunt întotdeauna stringuri

## Accesarea proprietăților unui obiect

Se face în două feluri:
1. obiect.proprietate
2. obiect\["proprietate"\]

## Accesarea metodelor

1. obiect.metoda()
2. obiect\["metoda"\]()

Atunci când invoci o metodă folosind notația cu punct (dot notation), ai acces la proprietățile obiectului folosind `this`. Trebuie reținut faptul că `this` se referă la obiectul pentru care este invocată metoda.

Pentru că sintaxa `[".."]` folosește valoarea unui **string**, acest lucru înseamnă că o secvență de cod poate fi folosită pentru a construi valoarea acelui string:

```js
var stegulet = true;
var obiect = {
	a: 2000
};

var indexul;

if (stegulet) {
	indexul = "a";
};

console.log( obiect[indexul] ); // 2
```

Dacă pentru accesare se va folosi orice altceva în afară de stringuri, numărul sau obiectul vor fi transformate în stringuri (folosindu-se mecanismul de coercion).

ES6 introduce o nouă sintaxă care ușurează modul de redenumire dinamică a cheilor unui obiect. Până acum, acest lucru se făcea astfel:

```js
var numeCheieNou = "special";

var obi = {
	cheie1: 10,
	cheie2: "ceva"
};

obi[numeCheieNou] = 1000;
obi; // Object { cheie1: 10, cheie2: "ceva", special: 1000 }
```

ECMAScript 2015 propune următoarea sintaxă:

```js
var numeCheieNou = "special";

var obi = {
	cheie1: 10,
	cheie2: "ceva",
	[numeCheieNou]: 1000
};
```
