To create a separate bundle containing React and ReactDOM (the libraries you rely on) so that your main application code doesn't repeat these dependencies, you should follow these steps:

### 1. Install `webpack` and `webpack-cli` for bundling

Since your current setup uses Babel directly on files, for creating separate bundles, it's more manageable to use Webpack. Here's how:

```bash
npm install --save-dev webpack webpack-cli
```

### 2. Create a `webpack.config.js` for bundling React and your app

Set up a webpack configuration with multiple entry points:

- One for React (`all_react.js`)
- One for your app code

```js
// webpack.config.js
const path = require('path');

module.exports = {
  mode: 'production', // or 'development' for debugging
  entry: {
    // Entry for React libraries
    all_react: ['react', 'react-dom'],
    // Entry for your application code
    app: './my_app/static/js/index.js', // Adjust path as needed
  },
  output: {
    filename: '[name].bundle.js', // produces all_react.bundle.js and app.bundle.js
    path: path.resolve(__dirname, 'dist'), // output directory
    clean: true, // cleans folder before build
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/, // handle JS & JSX files
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react']
          }
        }
      }
    ],
  },
  optimization: {
    splitChunks: {
      // Avoid duplication of React in main bundle
      cacheGroups: {
        reactVendor: {
          test: /[\\/]node_modules[\\/](react|react-dom)[\\/]/,
          name: 'all_react',
          chunks: 'all',
        },
      },
    },
  },
};
```

### 3. Run Webpack to generate the bundles

Modify your `package.json` scripts:

```json
"scripts": {
  "build": "webpack --config webpack.config.js"
}
```
Then run:

```bash
npm run build
```

### 4. Usage in HTML

In your HTML template, include the React bundle first, then your app code:

```html
<script src="/dist/all_react.bundle.js"></script>
<script src="/dist/app.bundle.js"></script>
```

This setup ensures:

- `all_react.bundle.js` contains React & ReactDOM, referenced everywhere.
- `app.bundle.js` contains your application code that depends on React, which assumes React is already loaded on the page.

### Summary:

- Use `webpack` with multiple entry points.
- Extract React libraries into a separate bundle.
- Load dependencies first in your HTML.

---

### Notes:
- Make sure your server serves the `/dist` directory correctly.
- Adjust paths according to your project structure.
- You might also consider **DLLPlugin** or **externals** in webpack if you want even more control over vendor libraries.

Let me know if you'd like a complete example with a minimal setup or further customization!