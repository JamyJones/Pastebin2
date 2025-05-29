You can achieve this by configuring Webpack to transpile, bundle, and minify your JavaScript code while ensuring the output is stored in the `dist/` directory. Below is a professional Webpack setup that includes Babel for ES6 transpilation and optimizations for production.

### Steps to Set Up Webpack:

1. **Install dependencies:**
   You will need Webpack, Babel, and the necessary loaders/plugins.

   ```sh
   npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env clean-webpack-plugin terser-webpack-plugin
   ```

2. **Create a Webpack configuration file (`webpack.config.js`):**

   ```js
   const path = require('path');
   const { CleanWebpackPlugin } = require('clean-webpack-plugin');
   const TerserPlugin = require('terser-webpack-plugin');

   module.exports = {
       entry: path.resolve(__dirname, 'static/js/index.js'), // Entry point
       output: {
           path: path.resolve(__dirname, 'dist'),
           filename: 'bundle.js', // Output file
           publicPath: '/static/js/', // Flask-served static files
       },
       module: {
           rules: [
               {
                   test: /\.js$/,
                   exclude: /node_modules/,
                   use: {
                       loader: 'babel-loader',
                       options: {
                           presets: ['@babel/preset-env'], // Transpile ES6+
                       },
                   },
               },
           ],
       },
       plugins: [
           new CleanWebpackPlugin(), // Cleans the output directory before building
       ],
       optimization: {
           minimize: true,
           minimizer: [new TerserPlugin()], // Minification plugin
       },
       mode: 'production', // Production mode enables optimizations
   };
   ```

3. **Update Babel configuration (if needed in `.babelrc` or package.json):**
   
   ```json
   {
       "presets": ["@babel/preset-env"]
   }
   ```

4. **Build the project with Webpack:**
   Run the following command to transpile and minify your JavaScript files:

   ```sh
   npx webpack
   ```

### Flask Considerations:
Since Flask serves static files, ensure that the `dist/` directory is mapped correctly in your Flask app:

```python
from flask import Flask, send_from_directory

app = Flask(__name__, static_folder="dist")

@app.route('/static/js/<path:filename>')
def static_files(filename):
    return send_from_directory('dist', filename)

if __name__ == '__main__':
    app.run(debug=True)
```

This setup ensures:
- All ES6 modules are properly transpiled.
- The bundled and minified file is stored in the `dist/` directory.
- Flask serves the final processed JS file correctly.

Let me know if you need further clarification! 🚀