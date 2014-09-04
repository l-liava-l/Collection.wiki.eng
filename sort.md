**sort** сортирует исходную коллекцию по заданному указателю или условию.

## Интерфейс

```js
sort(opt_fieldOrParams) { return ?; }
```

### Аргументы

1. `($$CollectionFilter|function(this:Collection, ?): ?|Object)=` `opt_fieldOrParams` — [указатель](https://github.com/kobezzza/Collection/wiki/%D0%A3%D0%BA%D0%B0%D0%B7%D0%B0%D1%82%D0%B5%D0%BB%D0%B8) на ключ для сортировки, функция, которая возвращает значение для сортировки, **ИЛИ** объект параметров метода.

#### Доступные параметры

* `field`
* [id](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#id)
* [context](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#context)
* `reverse`
* [use](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#use)

##### field

```js
/**
 * @type {($$CollectionFilter|function(this:Collection, ?): ?)}
 */
```

Параметр **field** позволяет задать указатель на ключ, по которому будет осуществляться сортировка, или же функцию, которая возвращает значение для сортировки.

```js
var obj = [
	{name: 'Koba', age: 3},
	{name: 'Over', age: 4},
	{name: 'Drobila', age: 2}
];

$C(obj).sort({field: 'name'});
$C(obj).sort({field: function (el) { return $C(el).get('name'); }})
```

##### reverse

```js
/**
 * @type {boolean}
 * @default true
 */
```

Если параметр равен `true`, то сортировка происходит в обратном порядке.

```js
$C([2, 1, 4]).sort() // [1, 2, 4]
$C([2, 1, 4]).sort({reverse: true}) // [4, 2, 1]
```

### Примеры

```js
$C([4, 1, 2]).sort() // [1, 2, 4]
$C(new Set([4, 1, 2])).sort() // Set([1, 2, 4])
```