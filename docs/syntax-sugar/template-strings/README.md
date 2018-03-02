# Новые возможности JavaScript — Шаблонные строки

#### [Оглавление](../../README.md)

Шаблонные строки (шаблоны) являются строковыми литералами, допускающими использование выражений.

В ECMAScript 5 подобную функциональность приходилось писать вот так:

```javascript
// ECMAScript 5
function greet(name) {
  return 'Hello, ' + name + '!';
}

console.log(greet('John')); // Hello, John!
```

```javascript
// ECMAScript 5
var protocol = 'https';
var company = 'yandex';
var domain = 'ru';

console.log('Link: ' + protocol + '://' + company + '.' + domain); // Link: https://yandex.ru
```

```javascript
// ECMAScript 5
var tag = 'div';
var className = 'bem';
var children = 'Hello, world!';

function createElement(tagName, className, children) {
  return '<' + tagName + ' class="' + className + '">' + children + '</' + tagName + '>';
}

console.log(createElement(tag, className, children)); // <div class="bem">Hello, world!</div>
```

В ECMAScript 6, благодаря шаблонным строкам, всё проще:

```javascript
// ECMAScript 6
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet('John')); // Hello, John!
```

```javascript
// ECMAScript 6
const protocol = 'https';
const company = 'yandex';
const domain = 'ru';

console.log(`Link: ${protocol}://${company}.${domain}`); // Link: https://yandex.ru
```

Также стоит отметить, что шаблонные строки поддерживают многострочность.

```javascript
// ECMAScript 6
const tag = 'div';
const className = 'i-bem';
const children = 'Hello, world!';

function createElement(tagName, className, children) {
  return `
    <${tagName} class="${className}">
      ${children}
    </${tagName}>
  `;
}

console.log(createElement(tag, className, children)); // <div class="i-bem">Hello, world!</div>
```

В выражениях можно использовать различные операции (сложение, вычитание, и т.д.) и вызовы функций.  
Для того, чтобы убедиться, что мы действительно складываем числа, можно использовать `parseInt`.

```javascript
// ECMAScript 6
function add(a, b) {
  return `${a} + ${b} = ${parseInt(a) + parseInt(b)}`;
}

console.log(add(1, '2')); // 1 + 2 = 3
```

Шаблонные строки можно тегировать. Это позволяет изменять вывод шаблонов при помощи функции.
Её первый аргумент будет содержать массив строковых литералов, второй и последующие содержат
значения вычисленных выражений. В конце функция должна вернуть итоговую строку.

```javascript
// ECMAScript 6
const name = 'Tamik';

console.log(`Hello, ${name}!`); // Hello, Tamik!

function upperName(literals, ...values) {
  return literals[0] + values[0].toUpperCase();
}

console.log(upperName`Hello, ${name}!`); // Hello, TAMIK!
```
