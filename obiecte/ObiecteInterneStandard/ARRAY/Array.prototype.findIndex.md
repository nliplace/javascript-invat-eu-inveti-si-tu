# Array.prototype.findIndex()

Este returnat indexul unui element al array-ului dacă elementul din array satisface anumite condiții de test.
În caz contrar, adică elementul nu este găsit, este returnat -1.

```js
function isPrime(element, index, array) {
  var start = 2;
  while (start <= Math.sqrt(element)) {
    if (element % start++ < 1) {
      return false;
    }
  }
  return element > 1;
};

console.log([4, 6, 8, 12].findIndex(isPrime)); // -1, not found
console.log([4, 6, 7, 12].findIndex(isPrime)); // indexul este 2
```
