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

return a value of cluster's option

```js
var obj = $C();

obj.addCollection('foo', [1]);
obj.addAndSetCollection('bar', [1, 2, 3]);

obj.getCollection() // [1, 2, 3]
obj.getCollection('foo') // [1]
```

Set of methods:

* getCollections
* getFilters
* getContexts
* getNamespaces
* getVars

return the cluster itself.

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

return ID of active cluster's option (if there is one)

```js
var obj = $C();
obj.activeCollection() // null
obj.addAndSetCollection('bar', [1, 2, 3]);
obj.activeCollection() // 'bar'
```

, либо логическое значение (если id указан в вызове)
, or a logical value (if ID is specified in call)

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

return `true` if option exists in a cluster.

```js
var obj = $C();
obj.isCollectionExists('bar') // false
obj.addCollection('bar', [1, 2, 3]);
obj.isCollectionExists('bar') // true
```

## Addition
### Cluster of collections

Cluster of collections allow to encapsulate a set of collections in one instance of Collection.
It is necessary for a work with storages of data.

```js
var db = new Collection();

db.addCollection({
	users: ...
	goods: ...
});

db.saveAll();
```

### Cluster of filters

It should be noted: if filter marks as active then it will use as a default in all iteration methods, so it combined with explicitly specified filters,
You can determine filters like in iteration methods, namely like functions, string reducing or combined filters by ID.



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

// We will get a value with using filter extrim
db.get('extrim');

// Settign filter to active
db.setFilter('getKoba')

// Make a request with using of filter getByLvlAndAge,
// And because we have an active getKoba so the resulting request will be like getKoba && getByLvlAndAge

db.get('getByLvlAndAge');

// getKoba
db.get();
```

### Cluster of contexts

Context is a mechanism of Collection which allows to define the «start point» for a searching and selecting among elements.
The active context like active filter «combined» with specified explicitly.


```js
// Make a new collection. The catalog of music instruments:
// the primary level of the table is a hash-table. As a key we use an instrument type
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

// So now we select all guitars by fender company
// just direct get request =)
db.get('guitar > fender');

// Chose all models cheaper than 20000
db.get(':el.price < 20000'); // Error, the "price" option is not found,
                             // Because the count begins with the first element, not from guitar > fender
// A selection of options with the specified explicitly context.
db.get(':el.price < 20000', {context: 'guitar > fender'});

// OR

// to established a necessery start point we establish an active context
db.newContext('guitar > fender');

// Again do a get request
db.get(':el.price < 20000');

// When "get" set by pointer, it will also use an active context.
db.get('guitar > fender > 0'); // Error
db.get('0'); // Return requested element

db.get(':el.price < 20000', {context: 'guitar > fender'}); // Again error
```

Almost all methods of Collection work is limited by an active context (by default it is an empty string),
exception is a cluster's methods. For example: getCollection (always return a necessary collection regardless of context).

To avoid wrong situations you can set a cluster's context only by activity,
namely you can't transfer a context to forEach by ID.

in additional to standard methods there are a few extra **parent** and **parentContext** in cluster's context.
The first one change an active context on n (by default is 1) levels up and `parentContext` return a parent context.

```js
db.newContext('a > b > c');

db.parentContext(); // 'a > b'
db.parentContext(2); // 'a'

db.parent(2);
db.getContext(); // 'a'
```

### Cluster of variables

A temporary variables (var) — it is just an opportunity to save intermittent data, without external variables, inside a single instance of Collection.

```js
b.addVar({
	i: 20,
	tmpObj: [1, 2, 3]
});

// We can use a short record of variable call in string functions (instead of getVar)
db.get(':el == ${i}');
db.get(':el == this.getVar("i")');

db.get(':i == ${tmpObj}[0]');
```

Variables should be used to transfer parameters in string shorts of filters.
Then it will optimized effectively a JIT compiller of Collection.

```js

var db = $C([1, 2, 3]);

// AVOID
db.get(':el !== ' + 1);
db.get(':el !== ' + 2);

// CORRECTLY (${...} == #{...})
db.get({filter: ':el !== #{val}', vars: {val: 1}});
db.get({filter: ':el !== ${val}', vars: {val: 2}});
```

## cluster's options building

A **use** method allows us at the same time to set an active status for all cluster's parametrs by specified namespace (if such one exists).

```js
db.use('users');

// Will be search parameters users.w.sub.next, then: users.w.sub, users.w, users,
// point is delimiter
db.use('users.w.sub.next');
```


