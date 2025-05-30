To create a separate bundle for React libraries (`react` and `react-dom`) and include it in your project, follow these steps:

### 1. Setup Entry Point for React Libraries
Create a new JavaScript file, e.g., `my_app/static/js/react-bundle.js`, where you will import React and ReactDOM:

```js
// my_app/static/js/react-bundle.js
import React from 'react';
import ReactDOM from 'react-dom';

window.React = React;
window.ReactDOM = ReactDOM;
```

This way, React and ReactDOM are globally available as `window.React` and `window.ReactDOM`, which makes it easier to load separately.

---

### 2. Create a Bundling Script for React Libraries
Update your `package.json` scripts to generate the React bundle:

```json
"scripts": {
  "build": "babel my_app/static/js/index.js --out-file dist/index.min.js",
  "build-react": "webpack --entry ./my_app/static/js/react-bundle.js --output-path ./dist --output-filename all_react.js"
}
```

**Note:** Since you're already using Babel for transpiling, for bundling external libraries, it's more straightforward to use **Webpack**.

### 3. Set Up Webpack for React Bundling
Create a simple `webpack.config.js` in your project root (or wherever appropriate):

```js
const path = require('path');

module.exports = {
  entry: './my_app/static/js/react-bundle.js',
  output: {
    filename: 'all_react.js',
    path: path.resolve(__dirname, 'dist'),
  },
  mode: 'production', // Minifies output
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
        },
      },
    ],
  },
};
```

This configuration tells Webpack to bundle `react` and `react-dom` into a single file `dist/all_react.js`.

### 4. Install Webpack Dependencies
```bash
npm install --save-dev webpack webpack-cli babel-loader
```

### 5. Build the React Bundle
Run the command:

```bash
npm run build-react
```

This will generate `dist/all_react.js` containing React and ReactDOM.

---

### 6. Include React Bundle and Your App in HTML
In your HTML, add:

```html
<!-- Load React libraries first -->
<script src="/static/dist/all_react.js"></script>

<!-- Your app's bundle (processed with Babel) -->
<script src="/static/dist/index.min.js"></script>
```

Ensure the order is correct: **React libraries first**, then your transpiled code.

---

### 7. Update Babel Build Script as Needed
Your existing Babel script remains unchanged, just build your app code separately:

```json
"build": "babel my_app/static/js/index.js --out-file dist/index.min.js"
```

### **Summary**
- Use Webpack to bundle React and ReactDOM separately into `all_react.js`.
- Load this bundle before your application code in HTML.
- Use Babel to transpile your app JS code separately.

---

### **Optional: Using Module System Instead of Globals**
Alternatively, if you prefer to use ES Modules and a build system that supports modules, you can bundle React into your main bundle using Webpack and import React where needed, avoiding global variables—but the above method is simpler for traditional script inclusion.

---

Let me know if you'd like a full working example with all configuration files!