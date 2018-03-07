# Новые возможности JavaScript — Деструктурирующее присваивание

#### [Оглавление](../../README.md)

Деструктурирующее присваивание позволяет присваивать переменным свойства
массивов и объектов при помощи синтаксиса, который внешне напоминает литералы
массивов и объектов. Этот синтаксис может быть очень сжатым, но при этом более
выразительным, чем традиционный доступ к переменным.

Без деструктурирующего присваивания можно обратиться к первым двум элементам
массива так:

```javascript
// ECMAScript 5
var array = [{}, {}];

var firstElement = array[0];
var secondElement = array[1];
```

С деструктурирующим присваиванием эквивалентный код становится более лаконичным и
читаемым:

```javascript
// ECMAScript 6
const array = [{}, {}];

const [firstElement, secondElement] = array;
```

Также можно собрать все последние элементы массива используя [&laquo;остаточный&raquo; параметр](../fn-parameters/README.md):

```javascript
// ECMAScript 6
const [first, ...rest] = [1, 2, 3];

console.log(rest);
// Ожидаемый результат: [2, 3]
```

Присваивание несуществующего элемента обрабатывается корректно - как `undefined`. Например,
такое произойдет, если мы попытаемся обратиться к “лишнему” элементу массива:

```javascript
// ECMAScript 6
const array = [];

const [first, ...rest] = array;

console.log(first);
// Ожидаемый результат: undefined

console.log(rest);
// Ожидаемый результат: undefined
```

Деструктурирование позволяет сопоставлять переменным различные поля объектов.
Указав имя поля, а через двоеточие переменную, с которой оно сопоставляется,
мы получим переменную, которой присвоено значение поля.

```javascript
// ECMAScript 6
const person = {
  name: 'Tamik',
  age: 19,
};

const {name: firstName, age: age} = person;

console.log(firstName);
// Ожидаемый результат: "Tamik"

console.log(age);
// Ожидаемый результат: 19
```

Это очень удобно, например, если надо развести совпадающие значения внутренних полей:

```javascript
// ECMAScript 6
const person = {
  firstName: {
    isFirst: true,
    text: 'Tamik',
  },
  secondName: {
    isFirst: false,
    text: 'Lokyaev',
  },
  age: 19,
};

const {firstName: {text: firstName}, secondName: {text: secondName}, age} = person;

console.log(firstName);
// Ожидаемый результат: "Tamik"

console.log(secondName);
// Ожидаемый результат: "Lokyaev"

console.log(age);
// Ожидаемый результат: 19
```

При совпадении имени свойства и переменной можно воспользоваться следующей синтаксической
конструкцией:

```javascript
// ECMAScript 6
const person = {
  name: 'Tamik',
  age: 19,
};

const = {name, age} = person;

console.log(name);
// Ожидаемый результат: "Tamik"

console.log(age);
// Ожидаемый результат: 19
```

Деструктурирование можно вкладывать и совмещать:

```javascript
// ECMAScript 6
const deepObj = {
  props: [
    'prop_id',
    {
      id: 1,
    }
  ],
};

const {props: [propId, {id}]} = deepObj;

console.log(propId);
// Ожидаемый результат: "prop_id"

console.log(id);
// Ожидаемый результат: 1
```

Если при деструктурировании обратиться к свойствам, которые не определены, будет
возвращено значение `undefined`.

```javascript
// ECMAScript 6
const obj = {};

const {prop} = obj;

console.log(prop);
// Ожидаемый результат: undefined
```

Также возможно указать значения по умолчанию на случай, если свойство, которое
нужно деструктурировать, может быть неопределено:

```javascript
// ECMAScript 6
const array = [];

const [missing = 'Empty cell'] = array;

console.log(missing);
// Ожидаемый результат: "Empty cell"
```

### Применение

Передача множества параметров в функцию всегда опасна: легко запутаться, какие
параметры передавать и в каком порядке. Объект-хэш решает проблему порядка, но
набор полей в этом хэше приходилось писать в комментариях функции - иначе сигнатура
метода становилась совсем непрозрачной. Деструктурирование помогает решать эту
проблему: структура объекта попадает в сигнатуру функции, при этом порядок
аргументов по-прежнему не важен:

```javascript
// ECMAScript 6
function makeRequest({url, params}) {
  // ...
}
```

При этом есть возможность задать любому свойству значение по умолчанию:

```javascript
// ECMAScript 6
function makeRequest({url, params = {}}) {
  // ...
}
```

#### Использование с протоколом итераторов

ECMAScript 6 также определяет протокол для работы с итераторами. При итерации `Map`
происходит получение пары `[key, value]`, которое можно деструктурировать, чтобы было
удобнее работать как с ключом, так и со значением:

```javascript
// ECMAScript 6
const map = new Map();

map.set(1, true);
map.set(2, false);

for (let [key, value] of map) {
  console.log(key, value);
}
// Ожидаемый результат: 1, true -> 2, false
```

Перебор только ключей:

```javascript
// ECMAScript 6
const map = new Map();

for (let [key] of map) {
  // ...
}
```

Перебор только значений:

```javascript
// ECMAScript 6
const map = new Map();

for (let [, value] of map) {
  // ...
}
```
