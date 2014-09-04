**push** добавляет новый элемент в конец исходной коллекции и возвращает объект вида:

* `boolean` `result` — true, если элемент был добавлен;
* `?` `key` — ключ или индекс добавленного элемента;
* `?` `value` — значение добавленного элемента;

## Интерфейс

```js
push(val, opt_keyOrParams) { return {result: boolean, key: ?, value: ?}; }
```

### Аргументы

1. `?` `val` — новый элемент.
2. `(?|Object)=` `opt_keyOrParams` — [ключ добавляемого свойства](https://github.com/kobezzza/Collection/wiki/add#key) (только для объектов) **ИЛИ** объект параметров метода.

#### Доступные параметры

* [key](https://github.com/kobezzza/Collection/wiki/add#key)
* [id](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#id)
* [context](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#context)

### Примеры

```js
var arr = [1];
$C(arr).push(2) // {result: true, key: 1, value: 2}
arr // [1, 2]

var set = new Set([1]);
$C(set).push(2) // {result: true, key: 1, value: 2}
set // Set([1, 2])
```