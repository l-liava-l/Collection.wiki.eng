**extend** расширяет свойства исходного объекта свойствами заданных и возвращает его в качестве ответа.

## Интерфейс

```js
Collection.extend(deepOrParams, target, ...args) { return Object; }
```

### Аргументы

1. `(boolean|Object)` `deepOrParams = false` — если параметр равен `true`, то свойства копируются рекурсивно **ИЛИ** объект параметров метода.

2. `Object` `target` — расширяемый объект.
3. `...Object` `args` — расширяющие объекты.

#### Доступные параметры

* `deep`
* `withAccessors`
* `withProto`
* `concatArray`
* `traits`

##### deep

```js
/**
 * @type {boolean}
 * @default false
 */
```

Если параметр равен `true`, то при расширении происходит глубокий анализ внутренней структуры объекта, т.е. свойства копируются рекурсивно.

```js
var obj = {
	foo: {
		a1: 1,
		a2: 2
	}
};

$C.extend({deep: true}, obj, {
	foo: {a1: 4}
});

obj.foo.a1 // 4
obj.foo.a2 // 2
```

##### withAccessors

```js
/**
 * @type {boolean}
 * @default false
 */
```

Если параметр равен `true`, то расширение объектов идёт с учётом аксессоров свойств.

```js
var obj = {
	foo: 1
};

$C.extend({withAccessors: true}, obj, {
	get bar() {
		return this.foo;
	}
});

obj.bar() // 1
```

##### withProto

```js
/**
 * @type {boolean}
 * @default false
 */
```

Если параметр равен `true`, то при глубоком расширении объекта учитываются свойства прототипа.

```js
var obj = Object.create({
	foo: {
		a1: 1,
		a2: 2
	}
});

$C.extend({withProto: true, deep: true}, obj, {
	foo: {a1: 4}
});

obj.foo.a1 // 4
obj.foo.hasOwnProperty('a1') // true

obj.foo.a2 // 2
obj.foo.hasOwnProperty('a2') // false
```

##### concatArray

```js
/**
 * @type {boolean}
 * @default false
 */
```

Если параметр равен `true`, то в случае глубокого расширения массива другим массивом будет происходить конкатенация.

```js
var obj = Object.create({
	foo: [1]
});

$C.extend({concatArray: true, deep: true}, obj, {
	foo: [2]
});

obj.foo // [1, 2]
```

##### traits

```js
/**
 * @type {boolean}
 * @default false
 */
```

Если параметр равен `true`, то расширение новым свойством происходит только тогда, когда в результирующим объекте оно отсутствует.

```js
var obj = {
	foo: 1
};

$C.extend({traits: true}, obj, {
	foo: 2,
	bar: 1
});

obj.foo // 1
obj.bar // 1

var obj2 = {
	foo: {a: 1, b: 2}
};

$C.extend({traits: true, deep: true}, obj2, {
	foo: {a: 2, c: 3}
});

obj.foo.a // 1
obj.foo.b // 2
obj.foo.c // 3
```