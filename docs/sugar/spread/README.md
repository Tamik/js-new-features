# Новые возможности JavaScript — Оператор `Spread`

Оператор `Spread` (так же известный как &laquo;оператор разворота&raquo;) позволяет разворачивать
элементы массива для передачи элементов в аргументы функции или в другой массив.

Например, нужно собрать один массив из двух разных. В современном JavaScript это возможно
благодаря оператору `Spread`, минуя использование метода `concat`.

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

console.log([arr1, arr2]); // [[1, 2, 3], [4, 5, 6]]

console.log([...arr1, ...arr2]); // [1, 2, 3, 4, 5, 6]
```

Это так же работает и с объектами:

```javascript
const obj1 = {
  propOne: 1,
  propTwo: 2,
};

const obj2 = {
  propThree: 3,
  propFour: 4,
};

console.log({obj1, obj2}); // { obj1: { propOne: 1, propTwo: 2 }, obj2: { propThree: 3, propFour: 4 } }

console.log({...obj1, ...obj2}); // { propOne: 1, propTwo: 2, propThree: 3, propFour: 4 }
```

`Spread`-оператор так же удобен для передачи массивов в качестве аргументов функции.

```javascript
const array = [1, 2, 3];

function add(a, b, c) {
  return a + b + c;
}

console.log(add(array)); // 1,2,3undefinedundefined

console.log(add(...array)); // 6
```
