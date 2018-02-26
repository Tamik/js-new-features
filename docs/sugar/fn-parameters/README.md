# Новые возможности JavaScript — Параметры функции

В современном JavaScript (начиная с ECMAScript 6) появилась возможность использовать
параметры по умолчанию и остаточные параметры у функций.

## Параметры по умолчанию

```javascript
function greet(name) {
  if (!name) {
    return `Hello, guest.`;
  }

  return `Hello, ${name}.`;
}

console.log(greet()); // Hello, guest.

console.log(greet('John')); // Hello, John.

console.log(greet(undefined)); // Hello, guest.
```

Если в качестве одного из аргументов не было передано значение, то
можно задать значение по умолчанию у данного аргумента.  
Это позволяет избавиться от проверок внутри функции.

```javascript
function greet(name = 'guest') {
  return `Hello, ${name}.`;
}

console.log(greet()); // Hello, guest.

console.log(greet('John')); // Hello, John.

console.log(greet(undefined)); // Hello, guest.
```

## Остаточные параметры

```javascript
function sum(...values) {
  return values.reduce((acc, item) => acc + item);
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```
