# Новые возможности JavaScript — Деструктурирующее присваивание

Деструктурирующее присваивание позволяет присваивать переменным свойства
массивов и объектов при помощи синтаксиса, который внешне напоминает литералы
массивов и объектов. Этот синтаксис может быть очень сжатым, но при этом более
восприимчивым, чем традиционный доступ к переменным.

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

Также можно собрать все последние элементы массива используя [&laquo;остаточный&raquo; параметр]():

```javascript
const [first, ...rest] = [1, 2, 3];

console.log(rest); // [2, 3]
```

При обращении к элементам массива, которые находятся за его границей или не
существуют, то в результате будет возвращено значение, что и при обычном обращении —
`undefined`.

```javascript
const array = [];

const [first, ...rest] = array;

console.log(first); // undefined

console.log(rest); // undefined
```

Деструктурирование объектов позволяет сопоставлять переменным различные свойства объектов.
Указав сопоставляемое свойство, а затем переменную, с которой оно сопоставляется.

```javascript
const person = {
  name: 'Tamik',
  age: 19,
};

const {name: firstName, age: age} = person;

console.log(firstName); // Tamik

console.log(age); // 19
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

Можно определить параметры функции принимая в качестве параметра единственный объект
с несколькими свойствами вместо того, чтобы выписывать их в качестве отдельных аргументов.
Для упрощения передачи параметров в функцию хорошо подходит деструктурирование.

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
