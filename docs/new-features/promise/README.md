# Новые возможности JavaScript — Обещания

#### [Оглавление](../../README.md)

Обещание (`Promise`) представляет собой конечный результат асинхронной операции. Это
наполнитель, в котором находится значение успешного результата или нематерилизуемой
причины отказа.

Зачем использовать обещания?

Обещания предоставляют простую альтернативу для выполнения, составления и управления
асинхронными операциями по сравнению с традиционными подходами на основании функций
обратного вызова. Они также позволяют обрабатывать асинхронно ошибки, используя
подходы, которые похожи на синхронный `try/catch`.

Обещание может быть в одном из трёх состояний:
- `Pending` — результат обещания пока не определён, потому что асинхронная операция
ещё не завершила свою работу;
- `Fulfilled` — асинхронная операция завершилась, обещание имеет значение;
- `Rejected` —  асинхронная операция завершилась с ошибкой и обещание никогда не
сбудется. В этом состоянии обещание имеет глагол _reason_, который указывает, из-за
чего произошла ошибка.

```javascript
// ECMAScript 5
function get(url, successFn, errorFn) {
  var request = new XMLHttpRequest();

  request.open('GET', url);

  request.onload = function () {
    if (request.status === 200) {
      successFn(request.data);
    } else {
      errorFn(request.statusText);
    }

    request.onerror = function () {
      errorFn(Error('Network error'));
    }
  }

  request.send();
}
```

```javascript
// ECMAScript 6
function getAsync(url) {
  return new Promise((resolve, reject) => {
    const request = new XMLHttpRequest();

    request.open('GET', url);

    request.onload = () => {
      if (request.status === 200) {
        resolve(request.data);
      } else {
        reject(Error(request.statusText));
      }
    };

    request.onerror = () => reject(Error('Network error'));

    request.send();
  });
}
```
