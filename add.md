**add** add new element to collection and return object:

* `boolean` `result` — true, if element was added;
* `?` `key` — key or index the added element;
* `?` `value` — value of the added element;

## Interface

```js
add(val, opt_keyOrParams) { return {result: boolean, key: ?, value: ?}; }
```

### Arguments

1. `?` `val` — new element.
2. `(?|Object)=` `opt_keyOrParams` — the key of the added property (only for objects) **OR** объект параметров метода.

#### Available parameters

* `key`
* `unshift`
* `create`
* [id](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#id)
* [context](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#context)

##### key

```js
/**
 * @type {?}
 */
```

The **key** parametr allows you to specify key to added element (only for object).

```js
var obj = {};
$C(obj).add(1, {key: 'foo'}) // {result: true, key: 'foo', value: 1}
obj // {foo: 1}
```

##### unshift

```js
/**
 * @type {boolean}
 * @default true
 */
```

If parametr is `true`, then element will be added in the beginning of the collection

```js
var arr = [1];
$C(arr).add(2, {unshift: true}) // {result: true, key: 0, value: 2}
arr // [2, 1]
```

##### create

```js
/**
 * @type {boolean}
 * @default true
 */
```

Если параметр равен `false`, то в случае отсутствия запрашиваемого свойства будет сгенерированно исключение,  иначе оно будет создано.

```js
var obj = {};
$C(obj).add(1, {context: 'foo > bar', key: 'value'}) /* {
	result: true, 
	key: 'value', 
	value: 1
} */

obj // {foo: {bar: {value: 1}}}
```

### examples

```js
var arr = [1];
$C(arr).add(2) // {result: true, key: 1, value: 2}
arr // [1, 2]

var set = new Set([1]);
$C(set).add(2) // {result: true, key: 1, value: 2}
set // Set([1, 2])
```
