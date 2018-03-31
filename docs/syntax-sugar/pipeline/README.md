# Новые возможности JavaScript — Оператор конвейера

Оператор конвейера, на момент написания этого материала, поддерживается лишь
в Firefox 58+, да и то, его нужно включать. Однако в Babel уже имеется
предложение по этому поводу.  
Код с таким оператором выглядит как команды `bash`.

```javascript
// ECMAScript 6
const square = n => n * n;
const increment = n => n + 1;

console.log(square(increment(square(2))));
// Ожидаемый результат: 25
```

```javascript
// ECMAScript Next
const square = n => n * n;
const increment = n => n + 1;

console.log(2 |> square |> increment |> square);
// Ожидаемый результат: 25
```

```javascript
// ECMAScript 6
const upperFirst = string => string[0].toUpperCase() + string.substring(1);
const dotEnd = string => `${string}.`;

const phrase = 'hello, world';

const result = dotEnd(upperFirst(phrase));

console.log(result);
// Ожидаемый результат: "Hello, world."
```

```javascript
// ECMAScript Next
const upperFirst = string => string[0].toUpperCase() + string.substring(1);
const dotEnd = string => `${string}.`;

const phrase = 'hello, world';

const result = phrase
  |> upperFirst
  |> dotEnd;

console.log(result);
// Ожидаемый результат: "Hello, world."
```

Использование с различными аргументами:

Оператор пайплайна не требует каких-либо специальных правил для использования функций с
множеством аргументов.

```javascript
// ECMAScript 6
const square = x => x * x;
const pow = (x, y) => Math.pow(x ** y);

const result = pow(square(2), 5);

console.log(result);
// Ожидаемый результат: 1024
```

```javascript
// ECMAScript Next
const square = x => x * x;
const pow => (x, y) => x ** y; // Оператор возведения в степень

const result = 2
  |> square
  |> (basis => pow(basis, 5));

console.log(result);
// Ожидаемый результат: 1024
```

Использование с `async`/`await`:

```javascript
// ECMAScript 6
async function f(x) {
  // ...
}

await f(x);
```

```javascript
// ECMAScript Next
async function f(x) {
  // ...
}

x |> await f;
```
