# Новые возможности JavaScript — `Array#includes`

В ECMAScript 5 для поиска требуемого элемента в массива приходилось использовать
метод `indexOf` или `some` (но мало кто знает о методах `some`/`every`).

Вот как это выглядело:

```javascript
const arr = [1, 2, 3, 4, 5];
const searchElement = 5;

const includes = arr.indexOf(searchElement) !== -1;

console.log(includes); // true
```

```javascript
const arr = [1, 2, 3, 4, 5];
const searchElement = 5;

const includes = arr.some(item => item === searchElement);

console.log(includes); // true
```

Однако в ECMAScript 7 появился метод: `includes`. В него достаточно передать
искомый элемент, и метод вернёт булево значение. В отличие от предыдущих двух методов
теперь сравнивать текущий элемент массива с искомым не надо.

```javascript
const arr = [1, 2, 3, 4, 5];
const searchElement = 5;

const includes = arr.includes(searchElement);

console.log(includes); // true
```
