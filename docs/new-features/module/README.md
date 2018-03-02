# Новые возможности JavaScript — Модули

#### [Оглавление](../../README.md)

Целью модулей ECMAScript 6 было создание формата, удобного как для пользователей
CommonJS, так и для пользователей AMD. В связи с этим они имеют такой же компактный
синтаксис, как и модули CommonJS. Но с другой стороны, они не такие динамичные.

Это даёт два основных преимущества:
- На этапе компиляции можно обнаружить ошибки, если импортировано что-то, что не
было предварительно экспортировано;
- Можно легко осуществить асинхронную загрузку модулей ECMAScript 6.

### Импорт

Ключевое слово `import`. Путь до файла указывается относительно директории, в которой
лежит файл, импортирующий другой модуль. Расширение опускается.

```javascript
// ECMAScript 6
import {APP_VERSION} from './path/to/module';

console.log(APP_VERSION); // 1.0
```

Также при импорте можно заменить название переменной на иное:

```javascript
// ECMAScript 6
import {APP_VERSION as version} from './path/to/module';

console.log(version); // 1.0
```

При надобности импортировать все сущности из одного модуля, можно воспользоваться
следующей конструкцией:

```javascript
// ECMAScript 6
import * as module from './path/to/module';

console.log(module.APP_VERSION); // 1.0

console.log(module.generateSequence(5)); // [0, 1, 2, 3, 4]
```

### Экспорт

Ключевое слово `export`, стоящее перед объявлением переменной (непосредственно
перед `var`, `let`, `const`), функции или класса экспортирует их в остальные
части приложения.

```javascript
// ECMAScript 6
const toExport = false;

export const APP_VERSION = 1.0;

export function generateSequence(length) {
  const array = [];

  for (let i = 0; i < length; i++) {
    array.push(i);
  }

  return array;
}
```

Модуль выше экспортирует константу `APP_VERSION` и [функцию-генератор](../generators/README.md) `generateSequence`.

### Экспорт по умолчанию

Иногда модуль экспортирует только одно значение (большой класс, например).
В таком случае удобно определить это значение как экспортируемое по умолчанию:

```javascript
// ECMAScript 6
export default class { // анонимный класс
  // ...
}
```

Синтаксис импорта таких значений аналогичный обычному импорту без фигурных скобок.

### Альтернатива встроенному экспорту

Если не хотите вставлять `export`-ы в код, то можно всё экспортировать позже,
например, в конце:

```javascript
// ECMAScript 6
const toExport = false;

const APP_VERSION = 1.0;

function generateSequence(length) {
  const array = [];

  for (let i = 0; i < length; i++) {
    array.push(i);
  }

  return array;
}

export {
  APP_VERSION,
  generateSequence,
}
```

### Изменение названия сущности при экспорте

```javascript
// ECMAScript 6
// ./app/moduleOne.js
export const APP_CONFIG = {
  version: 0.1,
};

export function getVersion(config) {
  return config.version;
}

// ./app/moduleTwo.js
export default function connectDb() {
  // ...
}

// ./app/index.js
export {
  APP_CONFIG as appConfig,
  getVersion,
} from './moduleOne';

export {default as initDb} from './moduleTwo';

// ./index.js
import {appConfig, getVersion, init} from './app';
```

### Встроенные модули

Другим вариантом использования может быть предотвращение того, чтобы переменные
становились глобальными. На данный момент, например, для этой цели лучше всего
использовать самовызывающуюся функцию.

В ECMAScript 6 вы можете использовать анонимный внутренний модуль:

```javascript
// ECMAScript 6
module {
  // ...
}
```

Кроме того, что такая конструкция проще с точки зрения синтаксиса, её содержание
автоматические отображается в `strict mode`.

Обратите внимание, что не обязательно осуществлять импорт внутри модуля.
Инструкция `import` может использоваться в контексте обычного скрипта.
