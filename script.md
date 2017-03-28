# Creating node packages using TypeScript
> The TypeScript compiler makes it super easy to create high quality NodeJS packages that can be used with compile time safety in other TypeScript packages.

We will go ahead an initialize our node package using `npm init` selecting the defaults

```
npm init -y
```

We will install the TypeScript compiler and save to our dev dependencies. This is the only package you need to compile and use TypeScript packages and is completely self contained.

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
* with declaration true the typescript compiler will automatically generate `.d.ts` declaration files.
* we will output all the js and declaration files to the `lib` folder
* finally we include all the files from `src` directory.

Now lets write some source code: 
* We will create an `src/index.ts`

We will export a simple `sum` function that takes two numbers and returns their sum

```js
export function sum(a: number, b: number) {
  return a + b;
}
```
Now to compile this package we will add a build script to our package.json.

```json
"build": "tsc -p ."
```
* A `build` target to compile TypeScript to JavaScript using our tsconfig.json.

Now on the command line you just invoke this target `npm run build` 

```sh
npm run build
```
Along with whatever your npm publishing process is for JavaScript e.g. I'll create a package release, push the tag upstream and then publish it on npm.

```sh
npm version patch && git push --follow-tags && npm publish
```

Using such pacakges is super easy.