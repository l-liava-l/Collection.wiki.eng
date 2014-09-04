Collection поддерживает модульную сборку библиотеки, но для этого вам нужно предварительно сделать следующие шаги:

1. Скачать и установить [node.js](http://nodejs.org/);
2. Склонировать репозитарий Collection

	```bash
	git clone https://github.com/kobezzza/Collection
	```

3. Установить зависимости через NPN

	```bash
	cd Collection
	npm install
	```

4. Скачать и установить [JRE](http://www.oracle.com/technetwork/java/index-jsp-138363.html);

5. Скачать [Google Closure Compiler](http://dl.google.com/closure-compiler/compiler-latest.zip) и поместить его в папку с Collection;

6. Открыть файл [builds.js](https://github.com/kobezzza/Collection/blob/master/builds.js) и закомментировать ненужные флаги в 

	```js
	'@build': true

	,'old': true // Поддержка старых браузеров
	,'map_set.keys': true // Полифил для работы .keys у Map / Set

	,'link': true
	,'filter.string': true
	,'filter.id': true

	,'static.toArray': true
	,'static.toString': true
	,'static.valueOf': true

	,'drivers:storage.indexeddb': true
	,'drivers:storage.localstorage': true // Драйвер для LocalStorage / SessionStorage

	,'cluster.new': true
	,'cluster.add': true
	,'cluster.set': true
	,'cluster.update': true
	,'cluster.drop': true
	,'cluster.context': true
	,'cluster.use': true

	,'single.add': true
	,'single.push': true
	,'single.unshift': true
	,'single.concat': true

	,'mult.some': true
	,'mult.every': true
	,'mult.get': true

	,'mult.set': true
	,'mult.addOrSet': true

	,'mult.remove': true
	,'mult.pop': true
	,'mult.shift': true

	,'mult.search': true
	,'mult.indexOf': true
	,'mult.lastIndexOf': true

	,'mult.map': true
	,'mult.filter': true

	,'mult.reduce': true
	,'mult.group': true

	,'sort': true
	,'reverse': true
	```

	, а после этого запустить команду

	```bash
	node build
	```

	(обновлённые файлы будут заменены в папке `/build`);

7. Что бы запустить тесты, то нужно предварительно запустить тестовый веб-сервер

	```bash
	node server
	```

	, а затем в браузере открыть `localhost:1337/tests/index.html`.