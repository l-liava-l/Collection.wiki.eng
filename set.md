**set** обновляет значение элементов исходной коллекции, которые подходят под заданное условие и возвращает массив объектов вида:

* `boolean` `result` — true, если элемент был обновлён;
* `?` `key` — ключ обновляемого элемента;
* `?` `value` — старое значение элемента.

Массив отсортирован в порядке обновления элементов. Если обновление было с параметром `mult = false` или по указателю, то возвращается сам объект.

## Интерфейс

```js
set(filterOrParams, val) { return [] || {result: boolean, key: ?, value: ?}; }
```

### Аргументы

1. `($$CollectionFilter|$$CollectionLink|Object)` `filterOrParams` — [фильтр](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#filter), [указатель](https://github.com/kobezzza/Collection/wiki/%D0%A3%D0%BA%D0%B0%D0%B7%D0%B0%D1%82%D0%B5%D0%BB%D0%B8) **ИЛИ** объект параметров метода, который соответствует [единому интерфейсу итераторов](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2).

2. `?` `val` — новое значение для обновления. Если параметр задан как функция, то он вызывается как callback и принимает следующие входные параметры:
	1. `el` — ссылка на текущий элемент коллекции
	2. `key` — ключ текущего элемента (для Set всегда равен `null`)
	3. `data` — ссылка на исходную коллекцию
	4. `i` — итерационный индекс, т.е. числовой номер элемента коллекции в текущей итерации
	5. `length` — функция, которая возвращает длину текущей коллекции (с учётом фильтров, вызов кешируется)

		*Функция может принимать один входной параметр: если он равен `true`, то длина коллекции вычисляется заново без учёта кеша.*

	6. `callee` — ссылка на саму функцию callback

	Возвращаемое значение функции (если такое есть, т.е. `!== undefined`) будет установлено как новое значение элемента.

	**this** внутри функции всегда указывает на исходный объект-экземпляр Collection, поэтому для передачи своего this необходимо использовать `.bind` (не желательно, т.к. работает очень медленно), `arrow function` или переменные замыкания.

#### Доступные параметры

* [filter](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#filter)
* [id](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#id)
* [mult](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#mult)
* [count](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#count)
* [from](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#from)
* [startIndex](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#startindex)
* [endIndex](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#endindex)
* [reverse](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#reverse)
* [inverseFilter](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#inversefilter)
* [notOwn](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#notown)
* [live](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#live)
* [use](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#use)
* [vars](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#vars)
* [context](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#context)
* [chain](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#chain)

`result` внутри фильтра ссылается на итоговый массив.

### Примеры

```js
// Обновление значения по указателю
$C([1, 2, 3]).set(0, 2) // {result: true, key: 0, value: 1}
$C([1, 2, 3]).set('eq(-1)', 1) // // {result: true, key: 2, value: 3}
$C({foo: {bar: 1}}).set('foo > bar', 2) // {result: true, key: 'bar', value: 1}

// Обновление значений по условию
$C([1, 2, 3]).set(function (el) {
	return el > 1;

}, function (el) { return el + 1; }) /* [
	{result: true, key: 1, value: 2}, 
	{result: true, key: 2, value: 3}
] */
```