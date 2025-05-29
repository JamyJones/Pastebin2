To configure Webpack for your JavaScript project, especially when using Flask to serve your application, you can follow these steps. This setup will transpile your ES6 code, bundle it, and output the minified code to a `dist/` directory.

### Step 1: Install Required Packages

First, ensure you have Node.js and npm installed. Then, navigate to your project directory and install the necessary packages:

```bash
npm init -y
npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env
```

### Step 2: Create Babel Configuration

Create a file named `.babelrc` in your project root to configure Babel:

```json
{
  "presets": ["@babel/preset-env"]
}
```

### Step 3: Create Webpack Configuration

Create a file named `webpack.config.js` in your project root with the following content:

```javascript
const path = require('path');

module.exports = {
  entry: './static/js/index.js', // Your main file
  output: {
    filename: 'bundle.js', // Output file name
    path: path.resolve(__dirname, 'dist'), // Output directory
    publicPath: '/static/js/', // Public path for serving files
  },
  module: {
    rules: [
      {
        test: /\.js$/, // Apply Babel to .js files
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
        },
      },
    ],
  },
  mode: 'production', // Set to 'development' for development mode
};
```

### Step 4: Update Your HTML

In your HTML file, make sure to include the bundled JavaScript file from the `dist/` directory:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your App</title>
</head>
<body>
    <script src="/static/js/bundle.js"></script>
</body>
</html>
```

### Step 5: Build Your Project

You can add a build script to your `package.json` to make it easier to run Webpack:

```json
"scripts": {
  "build": "webpack"
}
```

Now, you can run the following command to build your project:

```bash
npm run build
```

### Step 6: Serve Your Application

Make sure your Flask application is set up to serve static files correctly. You can run your Flask app, and it should serve the bundled JavaScript from the `dist/` directory.

### Summary

With this setup, Webpack will transpile your ES6 code from `static/js/index.js`, bundle it into `dist/bundle.js`, and minify it for production. You can adjust the configuration as needed for your specific project requirements.