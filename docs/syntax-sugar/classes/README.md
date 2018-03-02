# Новые возможности JavaScript — Классы

#### [Оглавление](../../README.md)

Классы в ECMAScript 6 — это синтаксический сахар, а не "честная" реализация,
как в других языках. По сути, это те же конструкторы функций
с использованием прототипов, только &laquo;приправленные&raquo; типичным
синтаксисом в виде классов из ООП.  
У классов, по сравнению с обычными функциями и переменными, есть особенности.
Во-первых, классы не поднимаются (т.н. &laquo;hoisting&raquo;) — поэтому
обращаться к классу можно только после его декларации. Во-вторых, тело класса
должно содержать только методы, но не свойства. Прототип, имеющий свойства,
обычно считается анти-паттерном.  
Также классы поддерживают геттеры и сеттеры в соответствии с
[объектными литералами](../object-literals/README.md).

```javascript
// ECMAScript 5
function A(prop) {
  this.prop = prop;
}

A.prototype.setProp = function(prop) {
  this.prop = prop;
}

A.prototype.getProp = function() {
  return this.prop;
}

var a = new A('example');

console.log(a.getProp()); // example

a.setProp('another example');

console.log(a.getProp()); // another example
```

```javascript
// ECMAScript 6
class A {
  constructor(prop) {
    this.prop = prop;
  }

  setProp(prop) {
    this.prop = prop;
  }

  getProp() {
    return this.prop;
  }
}

const a = new A('example');

console.log(a.getProp()); // example

a.setProp('another example');

console.log(a.getProp()); // another example
```

---

```javascript
// ECMAScript 5
function A() {
  // ...
}

function B() {
  // ...
}

A.prototype.prop = function () {
  return 1;
};

B.prototype.anotherProp = function() {
  return 2;
};

// Задаём наследование
B.prototype.__proto__ = A.prototype;

var b = new B();

console.log(b.prop); // 1

console.log(b.anotherProp); // 2
```

Однако стоит отметить, что доступ к ссылке `__proto__` не доступен в Internet Explorer до 10 версии,
и также является deprecated-способом для наследования. Для наследования в стандарте ES5 можно
использовать метод `Object.create`.

```javascript
// ECMAScript 5
function A() {
  // ...
}

function B() {
  // ...
}

A.prototype.prop = function () {
  return 1;
};

// Задаём наследование
B.prototype = Object.create(A.prototype);

B.prototype.anotherProp = function () {
  return 2;
};

var b = new B();

console.log(b.prop()); // 1

console.log(b.anotherProp()); // 2
```

```javascript
// ECMAScript 6
class A {
  // ...

  prop() {
    return 1;
  }
}

class B extends A {
  // ...

  anotherProp() {
    return 2;
  }
}

const b = new B();

console.log(b.prop()); // 1

console.log(b.anotherProp()); // 2
```

В классе-наследнике нужно вызвать `super()` до того, как обращаться к свойствам
через `this`, иначе произойдёт ошибка.

```javascript
// ECMAScript 6
class A {
  // ...
}

class B extends A {
  constructor() {
  }
  
  // ...
}

const b = new B(); // Ошибка!
```

Также желательно к прочтению: [&laquo;Новые #приватные поля классов в JavaScript&raquo;](https://medium.com/devschacht/javascripts-new-private-class-fields-c60daffe361b)
