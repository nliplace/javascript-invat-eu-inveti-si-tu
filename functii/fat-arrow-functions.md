# Funcții fat arrow

Sunt introduse odată cu ECMAScript 2015. Sunt soluția cea mai bună pentru funcțiile anonime. Nu au obiectul `arguments` și fac referință la obiectul `this` al funcției gazdă.
Funcțiile fat-arrow își au originile în expresiile lambda ale programării bazate pe funcții.

## Mantre

- Fat arrow sunt funcții.
- Funcțiile fat arrows sunt legate la scope-ul lexical. Nu mai este nevoie de trucul `var self = this` pentru a accesa contextul.
- nu au funcție internă [[Construct]] și astfel, nu pot crea obiecte cu `new`.
- nu exisă `this`, nici `arguments` și nici `super` sau `new.target`. Valorile pentru `this`, `super`, `arguments` și `new target` sunt luate de la funția în interiorul căreia este definit fat arrow-ul.
- Nu are proprietatea `prototype`.
- Nu poate modifica `this`-ul funcției gazdă.
- acceptă parametri și parametri rest.
- Lucrează cu un `this` fix, cel al funcției gazdă, fiind astfel eliminate multe surse de eroare. Dacă nu este într-o funcție gazdă, `this` va fi `undefined`.

Semnul care dă și denumirea de fat arrow este `=>` ceea ce înseamnă că funcția returnează rezultatul evaluării codului din funcție.

În funcție de scenariul de utilizare, un fat arrow poate fi scris în câteva moduri diferite.

## Un singur argument

Pentru un singur argument poți să nu mai pui parantezele:

```javascript
var x = valoare => valoare; x(1); // 1
```

## Zero, două sau mai multe argumente folosesc parantezele:

```javascript
var zero = () => 'sunt zero argumente'; zero();
var y = (unu, doi) => unu + doi; y(2,5); // 7
```

## Parametrii rest folosesc parantezele:

```javascript
var z = [1,2]; var w = (...z) => z; w(2,2); // Array [ 2, 2 ]
```

O funcție declarată clasic:

```js
[1,2,3].map(function(numar){ return numar * 2; });  // Array [ 2, 4, 6 ]
```

Funcția anonimă folosită de map, se poate rescrie folosind „fat arrow” astfel:

```js
[1,2,3].map( numar => numar * 2 );
```

Pentru a declara mai multe argumente se vor folosi parantezele:

```js
[1,2,3].map( (numar, index) => numar * 2 + index);
```

Dacă este nevoie de mai multe expresii nu numai să returnezi ceva simplu:

```js
[1,2,3].map( numar => {
  var multiplicare = 2 + numar;
  return numar * multiplicare;
} ); // Array [ 3, 8, 15 ]
```

Pentru a returna un obiect:

```js
[1,2,3].map( (numar, index) => ({numar: numar, indexul: index}) );
```

Arrow functions fac bindingul la contextul lexical stabilit.

```html
<button type="button" name="button" id="test">Testeaza this</button>
<script type="text/javascript">
  function Apasa(){
    this.stare = false;
    this.schimba = () => {
      this.stare = true;
    };
  };
  var ruptor = new Apasa();
  var element = document.getElementById('test');
  element.addEventListener('click', ruptor.schimba);
</script>
```

## Se aplică `call()`, `apply()` și `bind()`

Nu trebuie uitat faptul că fat arrows sunt funcții iar acestea moștenesc metodele lui `Function`.

```javascript
var x = (unu, doi) => unu + doi;
console.log(x.call(null, 1, 2)); // 3
console.log(x.apply(null, [1, 2])); // 3
var maLegLaObiectNull = x.bind(null, 1, 2); maLegLaObiectNull(); // 3
```
