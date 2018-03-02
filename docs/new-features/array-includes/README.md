# Новые возможности JavaScript — `Array#includes`

#### [Оглавление](../../../CONTENTS.md)

В ECMAScript 5 для поиска требуемого элемента в массиве приходилось использовать
метод `indexOf` или `some` (при этом мало кто знает о методах `some`/`every`).

Вот как это выглядело:

```javascript
// ECMAScript 5
const arr = [1, 2, 3, 4, 5];
const searchElement = 5;

console.log(arr.indexOf(searchElement) !== -1); // true
```

```javascript
// ECMASCript 5
const arr = [1, 2, 3, 4, 5];
const searchElement = 5;

console.log(arr.some(item => item === searchElement)); // true
```

Однако в ECMAScript 7 появился метод `includes`. В него достаточно передать искомый
элемент, и метод вернёт `boolean` значение. В отличие от предыдущих двух методов теперь
сравнивать текущий элемент массива с искомым не надо.  
При этом стоит отметить, что алгоритмическая сложность осталась прежней `O(n)`.

```javascript
// ECMAScript 7
const arr = [1, 2, 3, 4, 5];
const searchElement = 5;

console.log(arr.includes(searchElement)); // true
```
