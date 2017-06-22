Working branch: https://github.com/timkelty/yarn-order-bug/tree/working
Broken branch: https://github.com/timkelty/yarn-order-bug/tree/broken

The `package.json` in each branch is identical except for the order,
however the resulting `node_modules` end up different, and in this case end up
breaking this script:

Comparison: https://github.com/timkelty/yarn-order-bug/compare/broken...working

```
yarn start -- --use neutrino-preset-web
```

I've included the sourced `node_modules` directories for comparison.

You can recreate this by starting fresh:

```
rm -rf ./node_modules yarn.lock && yarn cache clean && yarn
```

The broken branch will give you an error like:

```
ERROR in   TypeError: Cannot read property 'request' of undefined

  - ExternalModuleFactoryPlugin.js:37 handleExternals
    [yarn-order-bug]/[html-webpack-plugin]/[webpack]/lib/ExternalModuleFactoryPlugin.js:37:33

  - ExternalModuleFactoryPlugin.js:46 next
    [yarn-order-bug]/[html-webpack-plugin]/[webpack]/lib/ExternalModuleFactoryPlugin.js:46:8

  - ExternalModuleFactoryPlugin.js:59 handleExternals
    [yarn-order-bug]/[html-webpack-plugin]/[webpack]/lib/ExternalModuleFactoryPlugin.js:59:7

  - ExternalModuleFactoryPlugin.js:79 ExternalModuleFactoryPlugin.<anonymous>
    [yarn-order-bug]/[html-webpack-plugin]/[webpack]/lib/ExternalModuleFactoryPlugin.js:79:5

  - NormalModuleFactory.js:246 applyPluginsAsyncWaterfall
    [yarn-order-bug]/[webpack]/lib/NormalModuleFactory.js:246:4

  - Tapable.js:196 NormalModuleFactory.applyPluginsAsyncWaterfall
    [yarn-order-bug]/[webpack]/[tapable]/lib/Tapable.js:196:70

  - NormalModuleFactory.js:230 NormalModuleFactory.create
    [yarn-order-bug]/[webpack]/lib/NormalModuleFactory.js:230:8

  - Compilation.js:382 Compilation._addModuleChain
    [yarn-order-bug]/[webpack]/lib/Compilation.js:382:17

  - Compilation.js:464 Compilation.addEntry
    [yarn-order-bug]/[webpack]/lib/Compilation.js:464:8

  - SingleEntryPlugin.js:22 SingleEntryPlugin.<anonymous>
    [yarn-order-bug]/[html-webpack-plugin]/[webpack]/lib/SingleEntryPlugin.js:22:15

  - Tapable.js:229 Compiler.applyPluginsParallel
    [yarn-order-bug]/[webpack]/[tapable]/lib/Tapable.js:229:14

  - Compiler.js:488
    [yarn-order-bug]/[webpack]/lib/Compiler.js:488:8

  - Tapable.js:131 Compiler.applyPluginsAsyncSeries
    [yarn-order-bug]/[webpack]/[tapable]/lib/Tapable.js:131:46

  - Compiler.js:481 Compiler.compile
    [yarn-order-bug]/[webpack]/lib/Compiler.js:481:7

  - Compiler.js:282 Compiler.runAsChild
    [yarn-order-bug]/[webpack]/lib/Compiler.js:282:7

  - compiler.js:70
    [yarn-order-bug]/[html-webpack-plugin]/lib/compiler.js:70:19

  - compiler.js:69 Object.compileTemplate
    [yarn-order-bug]/[html-webpack-plugin]/lib/compiler.js:69:10

  - index.js:47 Compiler.<anonymous>
    [yarn-order-bug]/[html-webpack-plugin]/index.js:47:40

  - Tapable.js:229 Compiler.applyPluginsParallel
    [yarn-order-bug]/[webpack]/[tapable]/lib/Tapable.js:229:14
```
