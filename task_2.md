# Задача №2

__Исходный код:__
```js
console.log(sum(2, 3)); // результат 5
console.log(sum(2)(3)(4)...); // сумма всех элементов
```

Итоговый код:

```js
function sum(a) {
  let arr = Array.prototype.slice.call(arguments); // создаем "трушный" массив, иначе reduce не сработает
  let currentSum = a; // для случая с множеством скобок создаем переменную для хранения суммы

  if (arr.length > 1) { // собственно, если много элементов в одних скобках – вернем результат reduce.
    return arr.reduce(function(sum, elem) {
      return sum + elem;
    }, 0);
  }

  // если же скобок много – создаем функцию, которую будем возвращать каждый раз при (3)(4)...
  function sumRec(b) {
    currentSum += b;
    return sumRec;
  };

  // при последнем вызове функция вернет себя же, поэтому придется преобразовать её в примитив
  sumRec.toString = function () {
    return currentSum;
  };

  return sumRec;
};
```

["К оглавлению"](README.md)

["< Так, стоп, а чо там в предыдущей"](task_1.md)

["Уперёд к следующей таске! >"](task_3.md)
