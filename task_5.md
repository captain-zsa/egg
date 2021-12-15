# Задача №5

__Исходный код:__
```js
function printOrderTotal(responseString) {
  var responseJSON = JSON.parse(responseString);

  responseJSON.forEach(function (item, index) {
    if (item.price = undefined) {
      item.price = 0;
    }

    orderSubtotal += item.price;
  });

  console.log("Стоимость заказа: "+ total > 0 ? "Бесплатно": total + " руб.");
};
```

## Рефакторинг:

Честно, код какой-то не весь тут будто... Ну ладно.

Первое, что меня смутило – `item.price = undefined` (присваивание, не сравнение). Ну окей, допустим тут забыли одно равно. Но зачем его "забывать" если можно сделать `if (!item.price)`? Ну и короткое раз на то пошло: `item.price = item.price ?? 0;`.

Далее `orderSubtotal += item.price;` если мы берем прям нынешний код (а я не знаю, используется ли где-то ещё item.price – вообще весь `forEach` сворачивается до `orderSubtotal += item.price ?? 0;`.

Но зачем нам `orderSubtotal` – тоже не ясно. Куда мы его деваем? Зачем `index` в функции `forEach`? Нужен ли нам вообще `forEach`? Как-то вырвано из контекста похоже.

Поэтому всё, что могу сделать в данной ситуации – жестко сократить:

```js
function printOrderTotal(responseString) {
  const responseJSON = JSON.parse(responseString);
  let orderSubTotal; // ну вот да, люблю так вот писать переменные в начале. Извиняйте))

  orderSubTotal = responseJSON.reduce((a, b) => a + (b.price ?? 0), 0);

  console.log('Стоимость заказа: ' + orderSubTotal ? orderSubTotal + ' руб.' : 'Бесплатно');
};
```

[К оглавлению](README.md)

[< Так, стоп, а чо там в предыдущей](task_4.md)

### The end
