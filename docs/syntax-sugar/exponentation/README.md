# Новые возможности JavaScript — Оператор возведения в степень

#### [Оглавление](../../README.md)

В ECMAScript 7 появился оператор возведения в степень.

`**` — это инфиксный оператор для возведения в степень.

```javascript
// ECMAScript 5
Math.pow(x, y);
```

вернёт тот же результат, что и

```javascript
// ECMAScript 7
x ** y
```

Примеры использования:

```javascript
// ECMAScript 7
const squared = 3 ** 2;

console.log(squared); // 9
```

```javascript
// ECMAScript 7
let squared = 3;

squared **= 2;

console.log(squared); // 9
```
