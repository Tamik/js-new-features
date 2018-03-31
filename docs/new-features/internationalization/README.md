# Новые возможности JavaScript — Интернационализация

#### [Оглавление](../../README.md)

Интернационализация — это задача, которую, в большинстве случаев, решить непросто,
но радует то, что в JavaScript имеется API интернационализации, хорошо
поддерживаемое большинством браузеров.

Примеры:

## Числовой формат

```javascript
// ECMAScript 6
const i18nEN = new Intl.NumberFormat("en-US");
const i18nDE = new Intl.NumberFormat("de-DE");
const i18nRU = new Intl.NumberFormat("ru-RU");

console.log(i18nEN.format(1234567.89));
// Ожидаемый результат: "1,234,567.89"
console.log(i18nDE.format(1234567.89));
// Ожидаемый результат: "1.234.567,89"
console.log(i18nRU.format(1234567.89));
// Ожидаемый результат: "1 234 567,89"
```

## Денежный формат

```javascript
// ECMAScript 6
const i18nUSD = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",
});
const i18nEUR = new Intl.NumberFormat("de-DE", {
  style: "currency",
  currency: "EUR",
});
const i18nRUR = new Intl.NumberFormat("ru-RU", {
  style: "currency",
  currency: "RUR",
});

console.log(i18nUSD.format(100200300.40));
// Ожидаемый результат: "$100,200,300.40"
console.log(i18nEUR.format(100200300.40));
// Ожидаемый результат: "100.200.300,40 €"
console.log(i18nRUR.format(100200300.40));
// Ожидаемый результат: "100 200 300,40 р."
```

## Формат даты

```javascript
// ECMAScript 6
const i18nEN = new Intl.DateTimeFormat("en-US");
const i18nDE = new Intl.DateTimeFormat("de-DE");
const i18nRU = new Intl.DateTimeFormat("ru-RU");

console.log(i18nEN.format(new Date("2018-04-05")));
// Ожидаемый результат: "4/5/2018"
console.log(i18nDE.format(new Date("2018-04-05")));
// Ожидаемый результат: "5.4.2018"
console.log(i18nRU.format(new Date("2018-04-05")));
// Ожидаемый результат: "05.04.2018"
```

Подробнее на [learn.javascript.ru](https://learn.javascript.ru/intl).
