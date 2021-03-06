# Next.js + Typescript

Use [Typescript](https://www.typescriptlang.org/) with [Next.js](https://github.com/zeit/next.js)

This plugin implements [@babel/preset-typescript](https://github.com/babel/babel/tree/master/packages/babel-preset-typescript) with Next.js.

## Installation

```
npm install --save @zeit/next-typescript
```

or

```
yarn add @zeit/next-typescript
```

## Usage

Create a `next.config.js` in your project

```js
// next.config.js
const withTypescript = require('@zeit/next-typescript')
module.exports = withTypescript({
  /* config options here */
})
```

Create a `.babelrc` in your project

```js
{
  "presets": [
    "next/babel",
    "@zeit/next-typescript/babel"
  ]
}
```

Create a `tsconfig.json` in your project

```json
{
  "compilerOptions": {
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "jsx": "preserve",
    "lib": ["dom", "es2017"],
    "module": "esnext",
    "moduleResolution": "node",
    "noEmit": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "preserveConstEnums": true,
    "removeComments": false,
    "skipLibCheck": true,
    "sourceMap": true,
    "strict": true,
    "target": "esnext"
  }
}
```

Optionally you can add your custom Next.js configuration as parameter

```js
// next.config.js
const withTypescript = require('@zeit/next-typescript')
module.exports = withTypescript({
  webpack(config, options) {
    return config
  }
})
```

### Type checking

If your IDE or code editor don't provide satisfying TypeScript support, or you want to see error list in console output, you can use [`fork-ts-checker-webpack-plugin`](https://github.com/Realytics/fork-ts-checker-webpack-plugin). It will not increase compile time because it forks type checking in a separate process

```js
// next.config.js
const withTypescript = require("@zeit/next-typescript")
const ForkTsCheckerWebpackPlugin = require('fork-ts-checker-webpack-plugin');

module.exports = withTypescript({
  webpack(config, options) {
    // Do not run type checking twice:
    if (options.isServer) config.plugins.push(new ForkTsCheckerWebpackPlugin())
    
    return config
  }
})
```
