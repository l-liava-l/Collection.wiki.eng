**concat** concatenates selected object with original collection and then return it (without regard to the additional context).

## Interface

```js
concat(obj, opt_id, opt_context) { return ?; }
```

### Arguments

1. `?` `obj` — object for concatenation.
2. `?string=` `opt_id = 'active'` — [original collection id](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#id).
3. `$$CollectionLink=` `opt_context` — additional [context](https://github.com/kobezzza/Collection/wiki/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2#context) for the original collection.

### Examples

```js
$C([1, 2, 3]).concat([4, 5]) // [1, 2, 3, 4, 5]
$C([1, 2, 3]).concat({foo: 1}) // [1, 2, 3, {foo: 1}]
$C(new Set([1])).concat([3, 4]) // Set(1, 3, 4)
```