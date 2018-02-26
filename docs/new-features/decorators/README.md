# Новые возможности JavaScript — Декораторы

#### [Оглавление](../../../CONTENTS.md)

Декораторы в JavaScript — это синтаксический сахар, который позволяет упрощённо вызывать
функции высшего порядка*.  
Декораторы в ECMAScript 7 могут работать с классами и дескрипторами свойств. Им автоматически
передаются дескриптор свойства и целевой объект. Имея доступ к дескриптору свойства, декоратор
может делать такие вещи как: добавление геттера к свойству, расширение поведения, которое могло
бы выглядеть громоздко без вынесения его в декоратор, автоматическая смена контекста вызова
функции на текущую сущность при первой попытке доступа к свойству.

На сегодняшний день декораторы могут быть определены как для определения классов, так и для
определения свойства.

```javascript
@readonly
class Person {
  // ...

  getAge() {
    return this.age;
  }
}
```

```javascript
class Person {
  // ...

  @readonly // Декоратор
  getAge() {
    return this.age;
  }
}
```

При добавлении метода к прототипу `Person` получится такое определение свойства:

```javascript
Object.defineProperty(Person.prototype, 'getAge', {
  value: specifiedFunction,
  enumerable: false,
  configurable: true,
  writable: true,
});
```

Видно, что на прототип вешается метод `getAge`. Этот метод не участвует в переборе свойств
объекта, его можно изменять и он доступен для записи. Но, допустим, что потребовалось явно
запретить возможность изменения реализации данного метода.  
Это возможно сделать при помощи декораторы `@readonly`, который, как понятно из названия,
давал бы доступ к такому методу &laquo;только для чтения&raquo; и запрещал бы любые
переопределения:

```javascript
function readonly(target, key, descriptor) {
  descriptor.writable = false;
  
  return descriptor;
}
```

Затем сам декоратор добавляется к методу следующим образом:

```javascript
class Person {
  // ...

  @readonly
  getAge() {
    return this.age;
  }
}
```

Теперь переопределить метод `getAge` у прототипа `Person` невозможно.

```javascript
class Person {
  // ...

  @readonly
  getAge() {
    return this.age;
  }
}

const person = new Person(19);

person.getAge = () => console.log(this.age); // Ошибка! Данный метод доступен только для чтения
```

Декоратор также может принимать параметры. В конечном итоге декоратор — это выражение,
поэтоу как `@readonly`, так и `@something(param)` должны работать.

Далее, давайте посмотрим на декорирование классов. Согласно предлагаемой спецификации,
декоратор принимает целевой конструктор. Например, мы могли бы создать декоратор
`@superhero` для класса `MySuperHero`:

Декорирование классов реализовано таким же способом. Согласно предлагаемой спецификации,
декоратор принимает целевой конструктор.
Рассмотрим следующий пример:

```javascript
function internalNetworkOnly(target) {
  target.internalNetworkOnly = true;
}

@internalNetworkOnly
class Permissions {
  // ...
}

console.log(Permissions.internalNetworkOnly); // true
```

Также можно дать возможность принимать декоратору параметры, тем самым превратив егоё
в фабричный метод:

```javascript
const params = {
  internalNetworkOnly: false,
  accessLevel: 0,
};

function setNetworkParams({internalNetworkOnly, accessLevel}) {
  return function(target) {
    target.internalNetworkOnly = internalNetworkOnly;
    target.accessLevel = accessLevel
  }
}

@setNetworkParams(params)
class Permissions {
  // ...
}

console.log(Permissions.internalNetworkOnly); // true
```

---

*Функция высшего порядка — это функция, которая может принимать другую функцию в качестве
аргумента или возвращать другую функцию в качестве результата.
