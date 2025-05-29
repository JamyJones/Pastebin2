To configure Webpack for transpiling and minifying your ES6 modules while ensuring the output is stored in the `dist/` directory, follow these steps:

### 1. Install Dependencies
First, ensure you have Webpack and Babel installed:

```sh
npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env
```

### 2. Configure Babel
Create a `.babelrc` file to configure Babel:

```json
{
  "presets": ["@babel/preset-env"]
}
```

### 3. Configure Webpack
Create a `webpack.config.js` file in your project root:

```js
const path = require("path");

module.exports = {
  entry: "./static/js/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  },
  mode: "production" // Enables minification
};
```

### 4. Update Package Scripts
Modify your `package.json` to include the Webpack build command:

```json
"scripts": {
  "build": "webpack"
}
```

### 5. Build Your Project
Run the following command to transpile and minify your code:

```sh
npm run build
```

After execution, Webpack will generate `bundle.js` inside the `dist/` folder.

Let me know if you need further clarification or additional configurations! 🚀 [[0]](https://github.com/Jameszjhe/redux-saga-demo/tree/f01386d596832d394e1e0a17b1023cd358d39c82/webpack.config.js) [[1]](https://github.com/andrzej-stasinski/academy3/tree/98dac1468ce8b24000b383e327c649d2b8686ee4/08_npm_es6_moduly/3_moduly/m5_zad_moduly/m51_ex_module_zad/webpack.config.js)



> [0] [](https://github.com/Jameszjhe/redux-saga-demo/tree/f01386d596832d394e1e0a17b1023cd358d39c82/webpack.config.js)
>
> [1] [](https://github.com/andrzej-stasinski/academy3/tree/98dac1468ce8b24000b383e327c649d2b8686ee4/08_npm_es6_moduly/3_moduly/m5_zad_moduly/m51_ex_module_zad/webpack.config.js)