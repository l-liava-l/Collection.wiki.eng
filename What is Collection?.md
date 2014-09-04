The standart JavaScript library has API for working with arrays, whith includes such methods as: `forEach`, `map`, `reduce` and etc. 
Using them, is good practice to make code better and easier

```js
// Return array there each element more than one
[1, 2, 3, 4].filter(function (el) { 
	return el > 1; 
});

// Return array there each element got by extracting the square root
[64, 16, 4].map(Math.sqrt);
```

It would be great to have the same API for other JavaScript data structures, leaving interface independed from the source data. It is such  functionality that Collection provides implements the set of the most important methods to work with all main types of collections.

```js
// Rewrite previous examples with Collection
$C([1, 2, 3, 4]).filter(function (el) { 
	return el > 1; 
});

$C([64, 16, 4]).map(Math.sqrt);

// And repeat for the table
$C({a: 1, b: 2, c: 3, d: 4}).filter(function (el) { 
	return el > 1; 
});

$C({a: 64, b: 16, c: 4}).map(Math.sqrt);
```

As you can see, difference between Collection and native methods in the call special constructor `$C` because majority methods of Collection make interface similar with array API 

Collection maintain the following types of data:
* Array (`Array`);
* Typed Array (partially);
* Tables «key-value» (`Object`, `Map`, `WeakMap`);
* List of unique values (`Set`, `WeakSet`);
* Strings;
* Generators;
* Iterators (on base `@@iterator` protocol).

Should be noted, what Collection does not implement polifils for old browsers, it's necessary to include polifils independently.
In addition to the standart functionality Collection introduces a several aditional methods and extends the standart methods is non standart features


```js
// remake collection elements in reverse order starting from the second element
// no more than 10 elements
$C(document.querySelectorAll('.foo')).forEach(function () {
	...
}, {
	reverse: true,
	startIndex: 2,
	count: 10
});

// Return elements array, where each element the original array, 
// which > 1, multiplied by 2
$C([1, 2, 3]).map(
	function (el) { 
		return el * 2; 
	}, 

	function (el) { 
		return el > 1; 
	}
);
```

Also implemented api for work with storages of data  (already have drivers for localStorage, sessionStorage и indexedDB) and several static methods, for example, [Collection.extend](https://github.com/kobezzza/Collection/wiki/extend) (more functionally than jQuery.extend). 
