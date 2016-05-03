# Clojures
---

## Dependințe cognitive
- funcții
- scope

## Definiții

Un clojure este un tip special de obiect care combină două lucruri: o funcție și mediul în care funcția a fost creată. Mediul constă din oricare variabilă care exista in-scope la momentul la care clojure-ul a fost creat (MDN - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures).
Acest obiect are acces la metodele prototype-ului funcției și la argumente precum call(), apply().

A closure is a special kind of object that combines two things: a function, and the environment in which that function was created.

Clojure este atunci când o FUNCȚIE ține minte scope-ul lexical chiar și atunci când este executată în afara acelui scope lexical (Kyle Simpson).

Un clojure este un obiect special care combină două lucruri: o funcție și mediul în care aceasta a fost declarată.
Mediul, adică scope-ul lexical constă din toate variabilele locale care erau în-scope la momentul în care s-a creat clojure-ul.

## Mantre
- JavaScript are un **scope lexical** generat la faza de compilare.
- Clojure-uri generează doar funcțiile.
- Un clojure permite accesarea variabilelor definite în funcția container.
- de fiecare dată când funcția externă este apelată, funcția internă este definită din nou. Codul funcției interne va fi identic, dar scope chain-ul asociat va fi diferit.
- un clojure nu poate accesa `this` al funcției container. În acest scop se folosește salvarea lui this într-o variabilă ```var self = this;``

## Analiză

Clojure-ul este folosit atunci când vrei să dai parametri unei funcții înainte ca acea funcție să fie executată.

Cazul 1 - funcție internă care folosește variabilele din scope

- ai o funcție iar în interior există altă funcție
- funcția internă are acces la tot ce-i în scope
- funcția internă se execută la când se execută și funcția container

```js
function localizare(loc){
  var localitate = 'Mihailești';

  function undeSunt(){
    console.log('Te afli la ' + localitate + ', ' + loc);
  };

  undeSunt();
};

localizare('La bar');
```

Cazul 2 - Funcțiile interne pot referi variabile definite în funcția container chiar dacă aceasta a returnat deja.

```js
function localizare(loc){
  var localitate = 'Mihailești';

  function undeSunt(){
    console.log('Te afli la ' + localitate + ', ' + loc);
  };

  return undeSunt();
};

var intrebare = localizare('La bar');
intrebare();
```

După cum se observă, funcția undeSunt() este executată în afara scope-ului lexical.
Astfel, este explicabil cum face „clojure” (prinde ca într-o plasă de pescuit) peste scope-ul înconjurător. Se poate apela la un moment ulterior în program.

Deci, un clojure este creat atunci când salvezi o funcție care are acces la contextul de execuție curent într-o variabilă în afara contextului de execuție curent.


```js
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
console.log(add5(2));  // 7
```

makeAdder() este cazul prezentat de Mozilla. Este perfect pentru a înțelege felul în care clojure-ul se formează în primă fază returnându-se funcția internă iar aceasta la rândul său returnând variabilele din mediu.
- makeAdder() generează scope-ul iar parametrul x devine variabilă locală atribuindu-se valoarea 5 la momentul invocării;
- makeAdder returnează o funcție iar variabila add5 devine referință către funcția internă. Astfel, add5 este o funcție a cărui parametru y devine variabilă locală în scope-ul creat de ea.
- add5(2) atribuie variabilei interne valoarea 2 și returnează suma dintre variabila locală și variabila peste care s-a făcut clojure din funcția container.

Spune documentația Mozilla că „în esență, makeAdder este o fabrică de funcții”.

Exemplu de referințe către obiecte care nu este un clojure (prezentat de Kyle Simpson):

```js

var obiect = (function(){
  var o = {test: "test"};
  return {obj: o} // obj ține o referință către obiectul o
})();

console.log(obiect. obj.test); // => test
```

## Utilitate

Este baza lui MODULE PATTERN prin care se realizează încapsularea și/sau ascunderea datelor.

## Erori
Este considerată a fi o eroare crearea de clojure-uri în bucle.

## Alonjă

Înțelegerea modului în care se face clojure vă va ajuta în înțelegerea lui Revealing Module Pattern.