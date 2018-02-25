# Новые возможности JavaScript — Шаблонные строки

Шаблонные строки (шаблоны) являются строковыми литералами, допускающими использование выражений.

В ECMAScript 5 подобную функциональность приходилось писать вот так:

```javascript
function greet(name) {
  return 'Hello, ' + name + '!';
}

console.log(greet('John')); // Hello, John!
```

```javascript
var protocol = 'https';
var company = 'yandex';
var domain = 'ru';

console.log('Link: ' + protocol + '://' + company + '.' + domain); // Link: https://yandex.ru
```

```javascript
var tag = 'div';
var class = 'bem';
var children = 'Hello, world!';

function createElement(tagName, className, children) {
  return '<' + tagName + ' class="' + className + '">' + children + '</' + tagName + '>';
}

console.log(createElement(tag, class, children)); // <div class="bem">Hello, world!</div>
```

В ECMAScript 6, благодаря шаблонным строкам, всё проще:

```javascript
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet('John')); // Hello, John!
```

```javascript
const protocol = 'https';
const company = 'https://yandex.ru';
const domain = 'ru';

console.log(`Link: ${protocol}://${company}.${domain}`); // Link: https://yandex.ru
```

Также стоит отметить, что шаблонные строки поддерживают многострочность.

```javascript
const tag = 'div';
const class = 'i-bem';
const children = 'Hello, world!';

function createElement(tagName, className, children) {
  return `
    <${tagName} class="${className}">
      ${children}
    </${tagName}>
  `;
}

console.log(createElement(tag, class, children)); // \n <div class="i-bem">\n   Hello, world!\n </div>\n
```

В выражениях можно использовать различные операции (сложение, вычитание, и т.д.) и вызовы функций.  
Для того, чтобы убедиться, что мы действительно складываем числа, можно использовать `parseInt`.

```javascript
function add(a, b) {
  return `${a} + ${b} = ${parseInt(a) + parseInt(b)}`;
}

console.log(add(1, '2')); // 1 + 2 = 3
```

Шаблонные строки можно тегировать. Это позволяет изменять вывод шаблонов при помощи функции.
Её первый аргумент будет содержать массив строковых литералов, второй и последующие содержат
значения вычисленных выражений. В конце функция должна вернуть итоговую строку.

```javascript
const name = 'Tamik';

console.log(`Hello, ${name}!`); // Hello, Tamik!

// Массив строковых литералов

function upperName(literals, ...values) {
  return literals[0] + values[0].toUpperCase();
}

console.log(upperName`Hello, ${name}!`); // Hello, TAMIK!
```
