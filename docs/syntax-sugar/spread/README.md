# Новые возможности JavaScript — Оператор разворота

#### [Оглавление](../../../CONTENTS.md)

Оператор `Spread` (так же известный как &laquo;оператор разворота&raquo;) позволяет разворачивать
элементы массива для передачи элементов в аргументы функции или в другой массив.

Например, нужно собрать один массив из двух разных. В современном JavaScript это возможно
благодаря оператору `Spread`, минуя использование метода `concat`.

```javascript
// ECMAScript 5
var array = [1, 2, 3];
var anotherArray = [4, 5, 6];

console.log([array, anotherArray]); // [[1, 2, 3], [4, 5, 6]]
```

```javascript
// ECMAScript 6
const array = [1, 2, 3];
const array = [4, 5, 6];

console.log([...array, ...anotherArray]); // [1, 2, 3, 4, 5, 6]
```

Это так же работает и с объектами:

```javascript
// ECMAScript 5
var obj = {
  one: true,
  two: true,
};

var anotherObj = {
  three: false,
  four: false,
};

console.log({obj, anotherObj}); // {obj: {one: true, two: true}, anotherObj: {three: false, four: false}}
```

```javascript
// ECMAScript 6
const obj = {
  one: true,
  two: true,
};

const anotherObj = {
  three: false,
  four: false,
};

console.log({...obj, ...anotherObj}); // {one: true, two: true, three: false, four: false}
```

`Spread`-оператор так же удобен для передачи массивов в качестве аргументов функции.

```javascript
// ECMAScript 5
var numbers = [1, 2, 3];

function add(a, b, c) {
  return a + b + c;
}

console.log(add(numbers)); // 1,2,3undefinedundefined
```

```javascript
// ECMAScript 6
const numbers = [1, 2, 3];

const add = (a, b, c) => (a + b + c);

console.log(add(...numbers)); // 6
```
