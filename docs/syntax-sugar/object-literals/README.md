# Новые возможности JavaScript — Расширение объектных литералов

#### [Оглавление](../../README.md)

Стандарт ECMAScript 6 добавил ряд улучшений для удобства работы с объектными
литералами. В первую очередь выделяются краткие свойства и возможность определения
методов без привязки анонимной функции.

Ранее при присваивании свойству значения одноимённой переменной приходилось писать
примерно такую запись:

```javascript
// ECMAScript 5
var a = 5;
var b = 5;

var obj = {
  a: a,
  b: b
};

console.log(obj); // {a: 5, b: 5}
```

Благодаря добавлению кратких свойств, теперь присваивание свойствам значения
одноимённых переменных происходит проще:

```javascript
// ECMAScript 6
const a = 5;
const b = 5;

const obj = {
  a,
  b,
};

console.log(obj); // {a: 5, b: 5}
```

Также при определении метода у объекта теперь не придётся присваивать значение со
ссылкой на функцию:

```javascript
// ECMAScript 5
var obj = {
  prop: true,
  fn: function(value) {
    console.log(value);
  }
}

obj.fn(false); // false
```

Теперь можно определять методы прямо в объекте:

```javascript
// ECMAScript 6
const obj = {
  prop: true,
  fn(value) {
    console.log(value);
  },
};

obj.fn(false); // false
```

Помимо прочего, появились геттеры и сеттеры:

```javascript
// ECMAScript 6
const obj = {
  __id: 1,
  get id() {
    return this.__id;
  },
  set id(value) {
    this.__id = value;
  },
};

console.log(obj.id); // 1

obj.id = 5;

console.log(obj.id); // 5

console.log(obj.__id); // 5
```

Также появилась возможность использовать вычисляемые свойства:

```javascript
// ECMAScript 6
const appConst = 'string';

const obj = {
  [appConst]: v => ({v}),
};

obj[`prefix_${appConst}`] = false;

console.log(obj.string('value')); // {v: 'value'}
console.log(obj.prefix_string); // false
```
