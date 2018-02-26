# Новые возможности JavaScript — Оператор возведения в степень

В ECMAScript 7 появился оператор возведения в степень.

`**` — это инфиксный оператор для возведения в степень.

```javascript
Math.pow(x, y);
```

вернёт тот же результат, что и

```javascript
x ** y
```

Примеры использования:

```javascript
const squared = 3 ** 2;

console.log(squared); // 9
```

```javascript
let squared = 3;

squared **= 2;

console.log(squared); // 9
```
