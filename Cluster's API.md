Cluster's API is a unified set of methods, which provides functionality for a work with collections. There are several clusters:

* collection — set of collections encapsulated in one instance of Collection;
* filter — set of filters, you can call them in "iterators";
* context — set of pointers;
* namespace — set of namespaces for a work with localstorage;
* var — set of variables encapsulated in one instance of Collection.

##  Option activity

If any of cluster options is active then it always uses by default.

### Keyword "active"
For universal access to active option in cluster's methodes you can use special keyword `active`.

## total API
### new_

Set of methods:

* newCollection
* newFilter
* newContext
* newNamespace
* newVar

add a new active option but don't add it to a cluster.

```js
var obj = $C();
obj.newCollection([1, 2, 3]);
obj.get() // [1, 2, 3]
obj.get({id: 'active'}) // [1, 2, 3]
```

### add_

Set of methods:

* addCollection
* addFilter
* addContext
* addNamespace
* addVar

add an option to a cluster but don't mark it active


there are 2 forms of calling method:

```js
var obj = $C();
obj.addCollection('foo', [1, 2, 3]);
obj.get({id: 'foo'}) // [1, 2, 3]
```

```js
var obj = $C();
obj.addCollection({foo: [1, 2, 3]});
obj.get({id: 'foo'}) // [1, 2, 3]
```

The second way allows you to add multiple values ​​to a cluster.

### addAndSet_

Set of methods:

* addAndSetCollection
* addAndSetFilter
* addAndSetContext
* addAndSetNamespace
* addAndSetVar

add an option to a cluster and mark it active

```js
var obj = $C();
obj.addAndSetCollection('foo', [1, 2, 3]);
obj.get() // [1, 2, 3]
obj.get({id: 'foo'}) // [1, 2, 3]
obj.get({id: 'active'}) // [1, 2, 3]
```

### set_

Set of methods:

* setCollection
* setFilter
* setContext
* setNamespace
* setVar

mark current option as active.

```js
var obj = $C();

obj.addCollection('foo', [1, 2, 3]);
obj.get() // []

obj.setCollection('foo');

obj.get() // [1, 2, 3]
obj.get({id: 'foo'}) // [1, 2, 3]
obj.get({id: 'active'}) // [1, 2, 3]
```

### drop_

Set of methods:

* dropCollection
* dropFilter
* dropContext
* dropNamespace
* dropVar

delete current option from a cluster

```js
var obj = $C();

obj.addCollection('foo', [1, 2, 3]);
obj.addAndSetCollection('bar', [1, 2, 3]);

// You can also use the keyword "active"

obj.dropCollection('foo', 'bar');
obj.get() // []
```

### update_

Set of methods:

* updateCollection
* updateFilter
* updateContext
* updateNamespace
* updateVar

update cluster's current option.

```js
var obj = $C();

obj.addCollection('foo', [1, 2, 3]);
obj.addAndSetCollection('bar', [1, 2, 3]);

obj.get() // [1, 2, 3]
obj.updateCollection('bar', [1]);

obj.get() // [1]
obj.get({id: 'bar'}) // [1]
```

### get_

Set of methods:

* getCollection
* getFilter
* getContext
* getNamespace
* getVar

возвращают значение кластерного параметра.
return value of cluster option

```js
var obj = $C();

obj.addCollection('foo', [1]);
obj.addAndSetCollection('bar', [1, 2, 3]);

obj.getCollection() // [1, 2, 3]
obj.getCollection('foo') // [1]
```

Пласт методов:
Method's set

* getCollections
* getFilters
* getContexts
* getNamespaces
* getVars

возвращают сам кластер.
returns the cluster itself

```js
var obj = $C();

obj.addCollection('foo', [1]);
obj.addCollection('bar', [1, 2, 3]);

obj.getCollections() // {foo: [1], bar: [1, 2, 3]}
```

### active_

Set of methods:

* activeCollection
* activeFilter
* activeContext
* activeNamespace
* activeVar

либо возвращают ИД активного параметра в кластере (если таковой есть)
Or return ID of active option of cluster (if there is)

```js
var obj = $C();
obj.activeCollection() // null
obj.addAndSetCollection('bar', [1, 2, 3]);
obj.activeCollection() // 'bar'
```

, либо логическое значение (если id указан в вызове)
, or logical value (if ID is specified in call)

```js
var obj = $C();
obj.addAndSetCollection('bar', [1, 2, 3]);
obj.activeCollection('bar') // true
obj.activeCollection('foo') // false
```

### is_Exists

Set of methods:

* isCollectionExists
* isFilterExists
* isContextExists
* isNamespaceExists
* isVarExists

возвращают `true` если заданный параметр существует в кластере.
return `true` if option exist in cluster

```js
var obj = $C();
obj.isCollectionExists('bar') // false
obj.addCollection('bar', [1, 2, 3]);
obj.isCollectionExists('bar') // true
```

## Addition
### Cluster of collections

Кластер коллекций позволяет инкапсулировать в одном экземпляре Collection множество коллекций.
В первую очередь это нужно для удобной работы с хранилищами данных.
Cluster of collections allow to encapsulate set of collections in one instance Collection
In the first place it need to work with storages of data

```js
var db = new Collection();

db.addCollection({
	users: ...
	goods: ...
});

db.saveAll();
```

### Filter's cluster Кластер фильтров

Следует помнить, что если фильтр указан активным, то он применяется всегда по умолчанию во всех итерационных методах, причём он «совмещается» с фильтрами, которые указываются явно.
Should be note: if filter is specified active then it will be use how default in all iteration methods, so it combined with filters, which is explicitly specified
Фильтры можно задавать также, как и в итерационных методах, т.е. как функции, строковые сокращения или составные фильтры по ИД.


```js
var db = new Collection([
	{name: 'Koba', age: 22, lvl: 80},
	{name: 'Over', age: 27, lvl: 90},
	{name: 'Drobila', age: 29, lvl: 85},
	{name: 'Nerzum', age: 20, lvl: 75}
]);

db.addFilter({
	getKoba: ':el.name === "Koba"',

	getByAge: function (el) {
		return el.age > 22;
	},

	getByLvlAndAge: '(:el.lvl >= 80) && getByAge',
	extrim: 'getByLvlAndAge || getKoba'
});

// Get value with use filter extrim Получим значения по фильтру extrim
db.get('extrim');

// Set filter to active Установка активного фильтра
db.setFilter('getKoba')

// Make request with use filter getByLvlAndAge Сделаем запрос по фильтру getByLvlAndAge,
// but because we use getKoba how active filter request have been type getKoba && getByLvlAndAge но т.к. у нас активный фильтр getKoba, то результирующий запрос будет типа getKoba && getByLvlAndAge

db.get('getByLvlAndAge');

// getKoba
db.get();
```

### Context's cluster Кластер контекстов

Контекст — это механизм Collection который позволяет задать «точку старта» для поиска и выборки элементов. Активный контекст, также как и фильтр, «совмещается» с указанным явно.

```js
// Создадим коллекцию, каталог музыкальных иснтрументов:
// первичный уровень таблицы будет хеш-таблицей, где ключ - тип инструмента
var db = new Collection({
	guitar: [
		fender: [
			{model: 'JAGUAR BLACKTOP HH RW BLK', price: 27921},
			{model: 'STRATOCASTER BLACKTOP HH MN BLK', price: 28390},
			{model: 'STANDARD TELECASTER ', price: 18518}
		],
		gibson: [
			{model: 'CUSTOM SHOP LES PAUL CUSTOM EB/GH', price: 159505},
			{model: 'LES PAUL STUDIO FIREBURST CHROME HARDWARE', price: 50525}
		]
	],
	bassGuitar: [
		fender: [
			{model: 'STANDARD JAZZ BASS RW Sunburst', price: 32205},
			{model: 'STANDARD PRECISION BASS', price: 30640}
		]
	]
});

// Теперь выберем все гитары фирмы fender
// для этого сделаем прямой запрос через get
db.get('guitar > fender');

// Выберем модели, дешевле 20-ти тысяч
db.get(':el.price < 20000'); // Ошибка, свойство price не найдено,
                             // Т.к. отсчёт идёт с самого первого объекта, а не с guitar > fender

// Выборка параметров с явным указанием контекста
db.get(':el.price < 20000', {context: 'guitar > fender'});

// ИЛИ

// Чтобы установить нужную точку отсчёта, установим активный контекст
db.newContext('guitar > fender');

// Теперь снова сделаем get запрос
db.get(':el.price < 20000');

// В случае задания в get по указателю, она также будет теперь отталкиваться от активного контекста
db.get('guitar > fender > 0'); // Ошибка
db.get('0'); // Вернёт запрашиваемый элемент

db.get(':el.price < 20000', {context: 'guitar > fender'}); // также будет ошибка
```

Почти все методы Collection работают в рамках активного контекста (по умолчанию равен пустой строке),
исключение составляют кластерные методы, например: getCollection (всегда будет возвращать искомую коллекцию вне зависимости от контекста).

Для избежания ошибочных ситуаций контекст из кластера можно устанавливать только с помощью активности,
т.е. нельзя например в forEach передать контекст по ИД.

В дополнение к стандартным методам у кластера контектов есть ещё несколько дополнительных: **parent** и **parentContext**.
Первый меняет активный контекст на n (по умолчанию на 1) уровней вверх, а метод parentContext возвращает родительский контекст.

```js
db.newContext('a > b > c');

db.parentContext(); // 'a > b'
db.parentContext(2); // 'a'

db.parent(2);
db.getContext(); // 'a'
```

### Кластер переменных

Временные переменные (var) — это просто возможность сохранять временные данные, не создавая внешних переменных, а внутри одного экземпляра Collection.

```js
b.addVar({
	i: 20,
	tmpObj: [1, 2, 3]
});

// Мы можем использовать сокращённую запись вызова переменной в строчных функциях (вместо getVar)
db.get(':el == ${i}');
db.get(':el == this.getVar("i")');

db.get(':i == ${tmpObj}[0]');
```

Переменные следует использовать для передачи параметров в строковые сокращения фильтров,
чтобы они могли эффективно оптимизироваться JIT компилятором Collection.

```js

var db = $C([1, 2, 3]);

// AVOID
db.get(':el !== ' + 1);
db.get(':el !== ' + 2);

// CORRECTLY (${...} == #{...})
db.get({filter: ':el !== #{val}', vars: {val: 1}});
db.get({filter: ':el !== ${val}', vars: {val: 2}});
```

## Сборка кластерных параметров

Метод **use** позволяет одновременно задать активное состояние для всех кластерных параметров по указанному пространству имён (если таковое есть).

```js
db.use('users');

// Будут искаться параметры users.w.sub.next, затем: users.w.sub, users.w, users,
// т.е. точка является разделителем
db.use('users.w.sub.next');
```


