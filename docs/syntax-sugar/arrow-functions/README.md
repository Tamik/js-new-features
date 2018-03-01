# Новые возможности JavaScript — Стрелочные функции

#### [Оглавление](../../../CONTENTS.md)

В ECMAScript 6 появился новый синтаксис функций.

```javascript
// ECMAScript 5
var numbers = [-2, -1, 0, 1, 2];

var positiveIntegers = numbers.filter(function(number) {
  return number > 0;
});

console.log(positiveIntegers); // [1, 2]
```

```javascript
// ECMAScript 6
const numbers = [-2, -1, 0, 1, 2];

const positiveIntegers = numbers.filter(number => number > 0);

console.log(positiveIntegers); // [1, 2]
```

Если вам нужна простая функция с одним аргументом, то синтаксис новых, стрелочных
функций, — это просто `идентификатор => выражение`. Не нужно печатать ни `function`,
ни `return`, ни круглых с фигурными скобками и точек с запятой.

```javascript
// ECMAScript 5
function add(a, b) {
  return a + b;
}

console.log(add(1, 2)); // 3
```

```javascript
// ECMAScript 6
const add = (a, b) => a + b;

console.log(add(1, 2)); // 3
```

Чтобы создать функцию с несколькими аргументами (или без аргументов, или с остаточными
параметрами, или с значениями по умолчанию, или с деструктурирующим присваиваиванием),
нужно просто добавить скобки вокруг списка аргументов.

```javascript
// ECMAScript 5
var array = [1, 2, 3, 4, 5];

var total = array.reduce(function(acc, item) {
  return acc + item;
}, 0);

console.log(total); // 15
```

```javascript
// ECMAScript 6
const array = [1, 2, 3, 4, 5];

const total = array.reduce((acc, item) => acc + item, 0);

console.log(total); // 15
```

Эффект при использовании [обещаний](../../new-features/promise/README.md) может быть
более заметным из-за нагромождения лишних блоков с фигурными скобами.

Без использования стрелочных функций:

```javascript
fetch(url)
  .then(function(result) {
    return JSON.parse(result);
  })
  .then(function(result) {
    console.log(result);

    return result;
  })
  .then(function(result) {
    return processResultData(result);
  });
```

С использованием стрелочных функций:

```javascript
fetch(url)
  .then(result => JSON.parse(result))
  .then(result => {
    console.log(result);

    return result;
  })
  .then(result => processResultData(result));
```

Также существует ещё одно отличие в поведении обычных и стрелочных функций.  
У стрелочных функций нет собственного значения `this`. Внутри стрелочной функции
`this` наследуется из окружающего лексического окружения (т. н. &laquo;лексический
контекст&raquo;).

```javascript
// ECMAScript 5
var person = {
  name: 'Tamik',
  showName: function() {
    return this.name;
  }
};

console.log(person.showName()); // Tamik
```

```javascript
// ECMAScript 6
const person = {
  name: 'Tamik',
  showName: () => this.name,
};

console.log(person.showName()); // undefined
```

```javascript
// ECMAScript 5
var person = {
  name: 'Tamik',
  showName: function() {
    setTimeout(function() {
      console.log(this.name)
    }, 1000);
  }
};

person.showName(); // undefined
```

```javascript
// ECMAScript 6
const person = {
  name: 'Tamik',
  showName: function() {
    setTimeout(() => console.log(this.name), 1000);
  },
};

person.showName(); // Tamik
```

Стрелочные функции позволяет избавиться от большинства проблем с замыканиям
(в которых не всегда &laquo;прозрачен&raquo; контекст).
Но запомните: обычные функции получают значение
`this` автоматически, неважно, нужно оно им, или нет. Стрелочные функции
получают `this` из лексического окружения, которого у функции может не оказаться.

В ECMAScript 6 танцы с бубном вокруг `this` в большинстве случаев не нужны,
если придерживаться этих правил:
- Использовать обычные функции для методов, которые будут вызываться с
использованием синтаксиса `object.method()`, таким способом эти функции получает
вменяемый `this` от вызывающего кода;
- Использовать стрелочные функции для всего остального. Это позволит вам избавиться
от лишних проблем с замыканием, с которым часто сталкиваются в функциях обратного
вызова (т.н. &laquo;callback&raquo;).

Также ECMAScript 6 предоставляет более краткий способ записи методов в литералах
объектов, так что код можно писать ещё проще. Подробнее об этом можно прочитать
в разделе [&laquo;Расширение объектных литералов&raquo;](../object-literals/README.md).

Ещё небольшие отличия стрелочных функций от обычных.

Работа с массивами и объектами несколько отличается:

```javascript
// ECMAScript 5
function getPerson() {
  return {
    name: 'Tamik',
    age: 19
  };
}

function getServices() {
  return ['Market', 'Maps', 'Music'];
}

console.log(getPerson()); // { name: 'Tamik', age: 19 }

console.log(getServices()); // ['Market', 'Maps', 'Music']
```

```javascript
// ECMAScript 6
const getPerson = () => ({
  name: 'Tamik',
  age: 19,
});

const getServices = () => (['Market', 'Maps', 'Music']);

console.log(getPerson()); // { name: 'Tamik', age: 19 }

console.log(getServices()); // ['Market', 'Maps', 'Music']
```

Стрелочная функция может быть IIFE*.

```javascript
// ECMAScript 5
(function() {
  console.log('IIFE');
})();
```

```javascript
// ECMAScript 6
(() => console.log('IIFE'))();
```

Стрелочные функции не могут быть конструкторами, с ними нельзя использовать
оператор `new`.

```javascript
// ECMAScript 6
const Person = () => console.log('Construct!');

const person = new Person(); // Ошибка! Person не является конструктором
```

Не рекомендуется использовать методы `bind`, `call` и `apply`, так как в стрелочных
функциях не имеет смысла изменять контекст. Присваивание контекста при помощи `bind`
создаёт новую функцию, которой присваивается заданный контекст. В итоге увеличивается
потребление памяти вашего приложения.

---

*IIFE (Immediately Invoked Function Expression) — функция, которая выполняется
сразу же после того как была определена.
