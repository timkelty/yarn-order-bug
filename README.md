Working branch: https://github.com/timkelty/yarn-order-bug/tree/working
Broken branch: https://github.com/timkelty/yarn-order-bug/tree/broken

The `package.json` in each branch is identical except for the order,
however the resulting `node_modules` end up different, and in this case end up
breaking this script:

```
yarn start -- --use neutrino-preset-web
```

I've included the sourced `node_modules` directories for comparison.

You can recreate this by starting fresh:

```
rm -rf ./node_modules yarn.lock && yarn
```
