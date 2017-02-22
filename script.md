> NOTES: 
- advantage 1: you get to use the latest JavaScript features e.g. arrow functions, ES6 exports, ES6 imports
- advantage 2: Syntactic checking. `asdf!@#`
- advantage 3: autocomplete (e.g. autocomplete the log function)


Here I have a simple log function that logs hello world, exported from utils.js
```
exports.log = function() {
  console.log('hello world');
}
```

I will go ahead and create a demo file that requires this function and uses it.
```
const utils = require('./utils');

utils.log();
```
Note that this is all just pure Node style JavaScript. Your can actually use TypeScript as a transpiler for pure JavaScript projects simply by adding a tsconfig.json file. 

Within our tsconfig.json file we set our target, the magic compiler option `"allowJs": true` which tells TypeScript to also support raw `.js` files, and `outDir` to provide an alternate location for *transpiled JavaScript*. Finally we include all the files in the src directory.

Now once I set this as my active project you can see that TypeScript picks up these source files, and I can even build these to our output `lib` directory.

One advantage of using TypeScript as a transpiler is that you get to use the latest JavaScript features e.g. 
arrow functions 
```js
exports.log = () => {
  console.log('hello world');
}
```
ES6 exports 
```js
export const log = () => {
  console.log('hello world');
}
```
and similarly es6 imports
```js
import { log } from './utils';
log();
```
and of course TypeScripts excellent autocomplete.

Additionally you get Syntactic checking.
```js
import { log } from './utils';
log();

asdf!@#
```

And finally the ability to mix and match JavaScript and TypeScript in the same project so you can upgrade your code base towards greater type safety.