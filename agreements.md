For «compiling» the library was used [Google Closure Compiler](https://github.com/google/closure-compiler) (GCC) in `ADVANCED_OPTIMIZATIONS` mode.
All methods of Collection have JSDoc description in [GCC standart](https://developers.google.com/closure/compiler/docs/js-for-compiler). Describing data types in the Wiki also uses this format. For optional parametrs was used prefix `opt_`.

Library was written on JavaScript (ECMAScript6) and uses the translator-polifil to ECMAScript3. 
All files with extension `.es6` is the source code written in ES6 from which the generated all `.js` ( ES3) files. translator is [es6-transpiler](https://github.com/termi/es6-transpiler).

The source code of library are folder [lib](https://github.com/kobezzza/Collection/tree/master/lib),and ready to use in folder [build](https://github.com/kobezzza/Collection/tree/master/build). 
Folders [tests](https://github.com/kobezzza/Collection/tree/master/tests) and [benchmarks](https://github.com/kobezzza/Collection/tree/master/benchmarks) contain unit tests and benchmarks.

For writing unit tests uses the library [Jasmine 2](https://github.com/pivotal/jasmine).