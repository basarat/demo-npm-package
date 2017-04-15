# Creating high quality node packages using TypeScript
> The TypeScript compiler makes it super easy to create high quality NodeJS packages that can be used with compile time safety in other TypeScript packages.

> Using JavaScript packages written in TypeScript can save you a lot of time digging around docs and then having to memorize the docs, in order to call the functions with the right spellings. This frees you up for a higher level of thinking and reasoning about logic and business requirements.

We will go ahead an initialize our node package using `npm init` selecting the defaults

```
npm init -y
```

Now to create a TypeScript package we need to install the TypeScript compiler. We will install it using NPM and save it to our dev dependencies. Note that the compiler completely self contained with zero external dependencies.

```
npm install typescript -D
```

We will also go ahead and create a tsconfig.json file for TypeScript configuration

```json
{
  "compilerOptions": {
    "declaration": true,
    "outDir": "lib"
  },
  "include": [
    "src"
  ]
}
```
* set our compiler options
* with declaration option set to true the typescript compiler will automatically generate `.d.ts` declaration files to allow seamless use of our package from other TypeScript projects.
* We will specify the outputDir for all the js and declaration files to be the `lib` folder
* finally we include all the files from `src` folder to the compilation context.

* We set this tsconfig as the active project in our IDE and create the main index file in the src folder which will be the entry point for our package.

* As a demonstration we will export a simple `sum` function that sums two numbers
* The function will take numbers a and b, and return their sum.

```js
/**
 * Sums two numbers
 */
export function sum(a: number, b: number) {
  return a + b;
}
```

* Beyond tsconfig, the only other thing we need to setup for TypeScript is our package.json.
* We point the JS main to the compiled lib/index
* We point the TS main to the compile lib/index
* A `build` target to compile TypeScript to JavaScript using our tsconfig.json.

```json
"build": "tsc -p ."
```

With this build target in place. We can compiler our project by simply running `npm run build`

```sh
npm run build
```
You can follow up this command with whatever process you currently use to publish your JavaSCript npm packages. e.g. I'll create a patch release and publish it on npm

```sh
npm version patch && npm publish
```

* Using such TypeScript packages is super easy. We simply jump to another NPM project

```
cd ../demo-ts-use
```

* And install our newly published TS package as a dependency.

```
npm install demo-ts -S
```

Note that to use this package we don't actually need TypeScript e.g.

* We can jump to the node console.
* Require the package.
* and use its exported members
* all without using TypeScript.

```bash
node
const pack = require('demo-ts');
pack.sum(1, 3);
.exit
```

So by creating a package using TypeScript you are not limiting your target audience in any way.

* That said a package written in TypeScript shines even brighter for people that use TypeScript.
* Lets jump to our IDE and open a TypeScript file within this project
* We can import the TypeScript module into this file
* Notice the 100% reliable package name import
* Also you get 100% reliable autocomplete when you import something from the module.

```js
import { sum } from "demo-ts";
```

* We also get nice autocomplete for using the imported function.
* Quick info for the function is also available automatically for consumers of our module.
* Consumer also get type checking e.g. `sum(1, 2)` works but `sum(1, 'hello')` complains

```js
sum(1, 2);
```
And the result is also type checked for us. We get quick info as well as autocomplete etc all by simply using TypeScript for JavaScript node modules.
### **(hover over result)**

```js
const result = sum(1, 2);
```
