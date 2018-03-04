# Новые возможности JavaScript — Новые методы `Array`

#### [Оглавление](../../README.md)

### `Array.includes`

В ECMAScript 5 для поиска требуемого элемента в массиве приходилось использовать
метод `Array.indexOf` или `Array.some` (при этом мало кто знает о методах `Array.some`/`Array.every`).

Вот как это выглядело:

```javascript
// ECMAScript 5
const array = [1, 2, 3, 4, 5];
const searchElement = 5;

console.log(array.indexOf(searchElement) !== -1); // true
```

```javascript
// ECMAScript 5
const array = [1, 2, 3, 4, 5];
const searchElement = 5;

console.log(array.some(item => item === searchElement)); // true
```

Однако в ECMAScript 7 появился метод `Array.includes`. В него достаточно передать искомый
элемент, и метод вернёт `boolean` значение. В отличие от предыдущих двух методов теперь
сравнивать текущий элемент массива с искомым не надо.  
При этом стоит отметить, что алгоритмическая сложность осталась прежней `O(n)`.

```javascript
// ECMAScript 7
const array = [1, 2, 3, 4, 5];
const searchElement = 5;

console.log(array.includes(searchElement)); // true
```

### `Array.find`

Метод `Array.find` производит поиск искомого элемента по массиву, и возвращает первое значение,
которое соответствует заданному условию в функции обратного вызова.

```javascript
// ECMAScript 6
const array = [0, 5, 10];

console.log(array.find(item => item > 1)); // 5
```

### `Array.findIndex`

Метод `Array.findIndex` работает таким же образом, как и `find`, но вместо значения искомого
элемента, соответствующему условию в функции обратного вызова, возвращает индекс
данного элемента.

```javascript
// ECMAScript 6
const array = [0, 5, 10];

console.log(array.findIndex(item => item > 1)); // 1
```

### `Array.fill`

Метод `Array.fill` позволяет заполнить массив заданным значением.

```javascript
// ECMAScript 6
const array = [1, 2, 3];

console.log(array.fill(5)); // [5, 5, 5]
```

```javascript
// ECMAScript 6
console.log(new Array(3).fill(5)); // [5, 5, 5]
```

При этом `fill` принимает 2 дополнительных аргумента: индекс позиций начала и конца
заполнения массива.

```javascript
// ECMAScript 6
const array = [0, 2, 4, 6, 8];

console.log(array.fill(10, 1, 3)); // [0, 10, 10, 10, 8]
```

### `Array#from`

Метод `Array#from` создаёт новый экземпляр массива `Array` из:

- &laquo;Псевдомассива&raquo;, имеющего свойство `length` и индексированные элементы.
Например, результат поиска по DOM методом `document.getElementsByClassName()`;
- Интерируемых объектов, содержимое которых можно получить по одному элементу за раз.
Массивы являются итерируемыми, так же как и новые структуры данных `Map` и `Set`.

```javascript
// ECMAScript 6
const list = document.querySelectorAll('.className');

Array.from(list).forEach(item => console.log(item));
```

```javascript
function Fn() {
  return Array.from(aguments);
}

console.log(Fn('param1', 'param2', 3, 4, 5)); // ['param1', 'param2', 3, 4, 5]
```

Вот так, например, можно создать массив со значениями элементов, соответствующих
индексу:

```javascript
// ECMAScript 6
const array = Array.from(new Array(5), (value, index) => index);

console.log(array); // [0, 1, 2, 3, 4]
```

### `Array.of`

Метод `Array.of` создаёт новый экземпляр массива `Array` из произвольного числа аргументов,
вне зависимости от числа или типа аргумента.

```javascript
// ECMAScript 6
const array = [1, 2, 3, 4, 5];

console.log(Array.of(1)); // [1]

console.log(Array.of(1, 2, 3)); // [1, 2, 3]

console.log(Array.of(array)); // [[1, 2, 3, 4, 5]]

console.log(Array.of(...array)); // [1, 2, 3, 4, 5]
```

---

Следующие методы помогают в повторении массивов:

- `Array.entries`
- `Array.keys`
- `Array.values`

Результатом каждого из вышеупомянутых методов является последовательность значений,
но они не возвращаются как массив; они раскрываются один за другим через итератор.

```javascript
// ECMAScript 6
const array = ['a', 'b', 'c'];

console.log(array.entries()); // [[0, 'a'], [1, 'b'], [2, 'c']]

console.log(array.keys()); // [0, 1, 2]

console.log(array.values()); // ['a', 'b', 'c']
```
