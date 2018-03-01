# Новые возможности JavaScript — Деструктурирующее присваивание

#### [Оглавление](../../../CONTENTS.md)

Деструктурирующее присваивание позволяет присваивать переменным свойства
массивов и объектов при помощи синтаксиса, который внешне напоминает литералы
массивов и объектов. Этот синтаксис может быть очень сжатым, но при этом более
выразительным, чем традиционный доступ к переменным.

Без деструктурирующего присваивания можно обратиться к первым двум элементам
массива так:

```javascript
var array = [{}, {}];

var firstElement = array[0];
var secondElement = array[1];
```

С деструктурирующим присваиванием эквивалентный код становится более лаконичным и
читаемым:

```javascript
const array = [{}, {}];

const [firstElement, secondElement] = array;
```

Также можно собрать все последние элементы массива используя [&laquo;остаточный&raquo; параметр](../fn-parameters/README.md):

```javascript
const [first, ...rest] = [1, 2, 3];

console.log(rest); // [2, 3]
```

Присваивание несуществующего элемента обрабатывается корректно - как `undefined`. Например,
такое произойдет, если мы попытаемся обратиться к “лишнему” элементу массива:

```javascript
const array = [];

const [first, ...rest] = array;

console.log(first); // undefined

console.log(rest); // undefined
```

Деструктурирование позволяет сопоставлять переменным различные поля объектов.
Указав имя поля, а через двоеточие переменную, с которой оно сопоставляется,
мы получим переменную, которой присвоено значение поля.

```javascript
const person = {
  name: 'Tamik',
  age: 19,
};

const {name: firstName, age: age} = person;

console.log(firstName); // Tamik

console.log(age); // 19
```

Это очень удобно, например, если надо развести совпадающие значения внутренних полей:

```javascript
const person = {
  firstName: {
    isFirst: true,
    text: 'Tamik',
  },
  secondName: {
    isFirst: false,
    text: 'Lokiaev',
  },
  age: 19,
};

const {firstName: {text: firstName}, secondName: {text: secondName}} = person;

console.log(firstName); // Tamik

console.log(secondName); // Lokiaev
```

При совпадении имени свойства и переменной можно воспользоваться следующей синтаксической
конструкцией:

```javascript
const person = {
  name: 'Tamik',
  age: 19,
};

const = {name, age} = person;

console.log(name); // Tamik

console.log(age); // 19
```

Деструктурирование можно вкладывать и совмещать:

```javascript
const deepObj = {
  props: [
    'prop_id',
    {
      id: 1,
    }
  ],
};

const {props: [propId, {id}]} = deepObj;

console.log(propId); // prop_id

console.log(id); // 1
```

Если при деструктурировании обратиться к свойствам, которые не определены, будет
возвращено значение `undefined`.

```javascript
const obj = {};

const {prop} = obj;

console.log(prop); // undefined
```

Также возможно указать значения по умолчанию на случай, если свойство, которое
нужно деструктурировать, может быть неопределено:

```javascript
const array = [];

const [missing = 'Empty cell'] = array;

console.log(missing); // Empty cell
```

### Применение

Передача множества параметров в функцию всегда опасна: легко запутаться, какие
параметры передавать и в каком порядке. Объект-хэш решает проблему порядка, но
набор полей в этом хэше приходилось писать в комментариях функции - иначе сигнатура
метода становилась совсем непрозрачной. Деструктурирование помогает решать эту
проблему: структура объекта попадает в сигнатуру функции, при этом порядок
аргументов по-прежнему не важен:

```javascript
function makeRequest({url, params}) {
  // ...
}
```

При этом есть возможность задать любому свойству значение по умолчанию:

```javascript
function makeRequest({url, params = {}}) {
  // ...
}
```

#### Использование с протоколом итераторов

ECMAScript 6 также определяет протокол для работы с итераторами. При итерации `Map`
происходит получение пары `[key, value]`, которое можно деструктурировать, чтобы было
удобнее работать как с ключом, так и со значением:

```javascript
const map = new Map();

map.set(1, true);
map.set(2, false);

for (let [key, value] of map) {
  console.log(key, value);
}
// 1, true
// 2, false
```

Перебор только ключей:

```javascript
const map = new Map();

for (let [key] of map) {
  // ...
}
```

Перебор только значений:

```javascript
const map = new Map();

for (let [, value] of map) {
  // ...
}
```
