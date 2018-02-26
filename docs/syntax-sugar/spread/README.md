# Новые возможности JavaScript — Оператор `Spread`

Оператор `Spread` (так же известный как &laquo;оператор разворота&raquo;) позволяет разворачивать
элементы массива для передачи элементов в аргументы функции или в другой массив.

Например, нужно собрать один массив из двух разных. В современном JavaScript это возможно
благодаря оператору `Spread`, минуя использование метода `concat`.

```javascript
const array = [1, 2, 3];
const anotherArray = [4, 5, 6];

console.log([array, anotherArray]); // [[1, 2, 3], [4, 5, 6]]

console.log([...array, ...anotherArray]); // [1, 2, 3, 4, 5, 6]
```

Это так же работает и с объектами:

```javascript
const obj = {
  one: true,
  two: true,
};

const anotherObj = {
  three: false,
  four: false,
};

console.log({obj, anotherObj}); // {obj: {one: true, two: true}, anotherObj: {three: false, four: false}}

console.log({...obj, ...anotherObj}); // {one: true, two: true, three: false, four: false}
```

`Spread`-оператор так же удобен для передачи массивов в качестве аргументов функции.

```javascript
const numbers = [1, 2, 3];

function add(a, b, c) {
  return a + b + c;
}

console.log(add(numbers)); // 1,2,3undefinedundefined

console.log(add(...numbers)); // 6
```
