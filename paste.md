To set up a JavaScript project using Webpack for transpiling and minifying your ES6 code, while serving it with Flask, you can follow these steps:

### Step 1: Install Required Packages

First, ensure you have Node.js and npm installed. Then, navigate to your project directory and install the necessary packages:

```bash
npm init -y
npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env
```

### Step 2: Configure Babel

Create a Babel configuration file named `.babelrc` in the root of your project:

```json
{
  "presets": ["@babel/preset-env"]
}
```

### Step 3: Configure Webpack

Create a Webpack configuration file named `webpack.config.js` in the root of your project:

```javascript
const path = require('path');

module.exports = {
  entry: './static/js/index.js', // Your main file
  output: {
    filename: 'bundle.js', // Output file name
    path: path.resolve(__dirname, 'dist'), // Output directory
  },
  module: {
    rules: [
      {
        test: /\.js$/, // Apply this rule to .js files
        exclude: /node_modules/, // Exclude node_modules
        use: {
          loader: 'babel-loader', // Use Babel loader
        },
      },
    ],
  },
  mode: 'production', // Set mode to production for minification
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

Run the following command to transpile and bundle your JavaScript files:

```bash
npm run build
```

This will create a `dist` directory containing the `bundle.js` file.

### Step 6: Serve with Flask

In your Flask application, ensure you serve the static files correctly. You can set up a route to serve your HTML file and include the bundled JavaScript:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True)
```

### Step 7: Create Your HTML File

In your `templates` directory, create an `index.html` file that includes the bundled JavaScript:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your App</title>
</head>
<body>
    <h1>Hello, Flask with Webpack!</h1>
    <script src="{{ url_for('static', filename='dist/bundle.js') }}"></script>
</body>
</html>
```

### Step 8: Run Your Flask Application

Finally, run your Flask application:

```bash
python app.py
```

Now, when you navigate to your Flask app in the browser, it should serve the HTML file, and the bundled JavaScript will be included and executed.

### Summary

1. Install Webpack and Babel.
2. Configure Babel and Webpack.
3. Create a build script in `package.json`.
4. Build your project to generate the `dist` directory.
5. Serve the bundled JavaScript with Flask.

This setup will allow you to transpile and minify your ES6 code effectively while serving it with Flask.