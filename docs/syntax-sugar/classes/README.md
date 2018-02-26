# Новые возможности JavaScript — Классы

#### [Оглавление](../../../CONTENTS.md)

Классы — это новый синтаксический сахар. По сути это те же конструкторы функций
с использованием прототипов, только приправленные типичным представлением в виде
классов из ООП.  
Классы не поднимаются (хойстинг). Тело класса может содержать только методы, но
не свойства. Прототип, имеющий свойства, обычно считается анти-паттерном.  
Так же поддерживают геттеры и сеттеры в соответствии с
[объектными литералами](../object-literals/README.md).

```javascript
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
