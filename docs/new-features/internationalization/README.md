# Новые возможности JavaScript — Интернационализация

#### [Оглавление](../../README.md)

Подробнее на [learn.javascript.ru](https://learn.javascript.ru/intl).

Примеры:

## Числовой формат

```javascript
// ECMAScript 6
const l10nEN = new Intl.NumberFormat("en-US");
const l10nDE = new Intl.NumberFormat("de-DE");
const l10nRU = new Intl.NumberFormat("ru-RU");

console.log(l10nEN.format(1234567.89)); // 1,234,567.89
console.log(l10nDE.format(1234567.89)); // 1.234.567,89
console.log(l10nRU.format(1234567.89)); // 1 234 567,89
```

## Денежный формат

```javascript
// ECMAScript 6
const l10nUSD = new Intl.NumberFormat("en-US", { style: "currency", currency: "USD" });
const l10nEUR = new Intl.NumberFormat("de-DE", { style: "currency", currency: "EUR" });
const l10nRUR = new Intl.NumberFormat("ru-RU", { style: "currency", currency: "RUR" });

console.log(l10nUSD.format(100200300.40)); // $100,200,300.40
console.log(l10nEUR.format(100200300.40)); // 100.200.300,40 €
console.log(l10nRUR.format(100200300.40)); // 100 200 300,40 р.
```

## Формат даты

```javascript
// ECMAScript 6
const l10nEN = new Intl.DateTimeFormat("en-US");
const l10nDE = new Intl.DateTimeFormat("de-DE");
const l10nRU = new Intl.DateTimeFormat("ru-RU");

console.log(l10nEN.format(new Date("2018-04-05"))); // 4/5/2018
console.log(l10nDE.format(new Date("2018-04-05"))); // 5.4.2018
console.log(l10nRU.format(new Date("2018-04-05"))); // 05.04.2018
```
