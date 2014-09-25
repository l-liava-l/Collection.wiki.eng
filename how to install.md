Collection was written on «pure» JavaScript and does not require dependences. Library can work with browsers (`IE 6+`, `FF`, `Chrome`) and with other environments:

* node.js;
* node-webkit;
* worker;
* addition to applications and etc.

The only one condition is permissibility of operation `new Function` (for example: if you writing an addition for Google Chrome you need to declare permission for eval in the manifest).

For installing in a browser need to download this [file](https://github.com/kobezzza/Collection/blob/master/build/collection.min.js) or [lite version](https://github.com/kobezzza/Collection/blob/master/build/collection.light.min.js)

```html
<!doctype html>
<html>
	<head>
		<title>...</title>
		<script src="collection.min.js"></script>
	</head>
	
	<body>
		...
	</body>
</html>
```

You can install the package using bower:

```bash
bower install --save collection.js
```
Library's file is located at the address:

* `collection.js/`
	* `build/`
		* `collection.min.js`

For node.js you can download Collection through the npm

```bash
npm install --save collection.js
```

```js
var collection = require('collection.js');
var $C = collection.$C;
```

Or just clone repository from github.

```bash
git clone https://github.com/kobezzza/Collection
```
