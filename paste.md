To configure Webpack for your JavaScript project, you will need to set up a few things, including the entry point, output directory, and loaders for transpiling your ES6 code. Below are the steps to achieve this:

### Step 1: Install Required Packages

First, make sure you have Node.js and npm installed. Then, navigate to your project directory and install Webpack and Babel along with the necessary presets and plugins:

```bash
npm init -y
npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env
```

### Step 2: Create Babel Configuration

Create a file named `.babelrc` in the root of your project directory to configure Babel:

```json
{
  "presets": ["@babel/preset-env"]
}
```

### Step 3: Create Webpack Configuration

Create a file named `webpack.config.js` in the root of your project directory. This file will contain the configuration for Webpack:

```javascript
const path = require('path');

module.exports = {
  entry: './static/js/index.js', // Your main file
  output: {
    filename: 'bundle.js', // The name of the output file
    path: path.resolve(__dirname, 'dist'), // Output directory
  },
  module: {
    rules: [
      {
        test: /\.js$/, // Apply this rule to .js files
        exclude: /node_modules/, // Exclude the node_modules directory
        use: {
          loader: 'babel-loader', // Use Babel loader
        },
      },
    ],
  },
  mode: 'production', // Set the mode to production for minification
};
```

### Step 4: Update Package.json Scripts

Add a build script to your `package.json` to easily run Webpack:

```json
"scripts": {
  "build": "webpack"
}
```

### Step 5: Build Your Project

Now you can build your project by running the following command in your terminal:

```bash
npm run build
```

This command will transpile and minify your code, and the output will be stored in the `dist/` directory as `bundle.js`.

### Step 6: Include the Output in Your HTML

Finally, make sure to include the generated `bundle.js` in your HTML file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Project</title>
</head>
<body>
    <script src="dist/bundle.js"></script>
</body>
</html>
```

### Summary

You have now configured Webpack to transpile and minify your ES6 code, with the output stored in the `dist/` directory. You can further customize your Webpack configuration as needed, such as adding plugins for additional features like CSS handling, image optimization, etc.