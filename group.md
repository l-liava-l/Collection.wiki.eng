**group** возвращает результат группировки элементов исходной коллекции по заданному указателю или условию.

## Интерфейс

```js
group(field, opt_filterOrParams) { return ?; }
```

### Аргументы

1. `($$CollectionLink|function(this:Collection, ...?): ?)` `field` — функция, которая вызывается для каждого элемента коллекции прошедшего фильтр и принимает следующие входные параметры:
	1. `el` — ссылка на текущий элемент коллекции
	2. `key` — ключ текущего элемента (для Set всегда равен `null`)
	3. `data` — ссылка на исходную коллекцию
	4. `i` — итерационный индекс, т.е. числовой номер элемента коллекции в текущей итерации
	5. `length` — функция, которая возвращает длину текущей коллекции (с учётом фильтров, вызов кешируется)

		*Функция может принимать один входной параметр: если он равен `true`, то длина коллекции вычисляется заново без учёта кеша.*

	6. `callee` — ссылка на саму функцию callback

	Возвращаемое значение функции будет использовано как ключ для группировки.

	**this** внутри field всегда указывает на исходный объект-экземпляр Collection, поэтому для передачи своего this необходимо использовать `.bind` (не желательно, т.к. работает очень медленно), `arrow function` или переменные замыкания.

	**ИЛИ** [указатель](https://github.com/kobezzza/Collection/wiki/%D0%A3%D0%BA%D0%B0%D0%B7%D0%B0%D1%82%D0%B5%D0%BB%D0%B8) на ключ для группировки.

2. `($$CollectionFilter|Object)=` `opt_filterOrParams` — [фильтр](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#filter) **ИЛИ** объект параметров метода, который соответствует [единому интерфейсу итераторов](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2).

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
* `saveKeys`
* `useMap`
* [chain](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#chain)

`result` внутри фильтра ссылается на итоговый объект.

##### saveKeys

```js
/**
 * @type {?boolean=}
 * @default false
 */
```

Если параметр равен `true`, то в качестве элементов группировки используются ключи.

```js
$C([
	{name: 'Koba', age: 22, lvl: 78},
	{name: 'Over', age: 27, lvl: 85},
	{name: 'Drobila', age: 27, lvl: 80},
	{name: 'Skins', age: 28, lvl: 79}

]).group('age', {saveKeys: true}) /* {
	22: [0],
	27: [1, 2],
	28: [3]
} */
```

##### useMap

```js
/**
 * @type {?boolean=}
 * @default false
 */
```

Если параметр равен `true`, то в качестве объекта для результата группировки будет использоваться Map, а не Object.

### Примеры

```js
$C([
	{name: 'Koba', age: 22, lvl: 78},
	{name: 'Over', age: 27, lvl: 85},
	{name: 'Drobila', age: 27, lvl: 80},
	{name: 'Skins', age: 28, lvl: 79}

]).group('age') /* {
	22: [
		{
			name : 'Koba',
			age : 22,
			lvl : 78
		}
	],

	27: [
		{
			name : 'Over',
			age : 27,
			lvl : 85
		},

		{
			name : 'Drobila',
			age : 27,
			lvl : 80
		}
	],

	28: [
		{
			name : 'Skins',
			age : 28,
			lvl : 79
		}
	]
} */
```