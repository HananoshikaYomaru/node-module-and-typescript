# node module testing + typescript 

```
 _________________
< I'm a moooodule >
 -----------------
        \   ^__^
         \  (oO)\_______
            (__)\       )\/\
             U  ||----w |
                ||     ||
```

## 1. use common js module 

```shell
node commonjs.js
```

## 2. use es module

you need to use mjs extension to specify the js as a module. Otherwise there will be an error. 

> Uncaught SyntaxError: Cannot use import statement outside a module`

```
node test.mjs 
```

the `mjs` tell node that this is a ES6 module
 
According to [enabling](https://nodejs.org/api/esm.html#esm_enabling) and [determining module system](https://nodejs.org/api/packages.html#packages_determining_module_system), Node.js treats JavaScript code as CommonJS modules by default. Authors can tell Node.js to treat JavaScript code as ECMAScript modules via the `.mjs` file extension, the `package.json` [`"type"`](https://nodejs.org/api/packages.html#packages_type) field, or the `--input-type=module` flag. See [Modules: Packages](https://nodejs.org/api/packages.html#packages_determining_module_system) for more details.

## 3. npm run script 

use a `script` attribute in `package.json`. This require `npm` installed.

# use with typescript 

in the `package.json`, there is such field 

```json
"scripts": {
    "dev": "ts-node test.ts"
},
```

when you run `npm run dev`, which is essentially `npm run ts-node test.ts`, npm will go inside the `node_modules` and find `ts-node` module and run that command. 

But what if you don't want to use `npm`? You can use run that `ts-node` command directly. How? 

When you check the `package.json`, you will see this module expose some commands. 

```shell
cat node_modules/ts-node/package.json
```

```json
"bin": {
    "ts-node": "dist/bin.js",
    "ts-script": "dist/bin-script-deprecated.js",
    "ts-node-script": "dist/bin-script.js",
    "ts-node-cwd": "dist/bin-cwd.js",
    "ts-node-transpile-only": "dist/bin-transpile.js"
  },
```

Therefore the `ts-node` command is correspond to the `dist/bin.js` file. Hence, you can run the command. 

```
node node_modules/ts-node/dist/bin.js test.ts
```





