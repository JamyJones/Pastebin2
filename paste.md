To achieve this, you need to set up Webpack properly to transpile your ES6 code, bundle it, minify it, and store it in the `dist/` directory. Here's how you can configure Webpack for your Flask-based application.

### Steps:
1. **Install Dependencies**  
   Ensure you have Node.js installed, then install Webpack and Babel-related packages:
   ```sh
   npm init -y
   npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env clean-webpack-plugin terser-webpack-plugin
   ```

2. **Configure Webpack (`webpack.config.js`)**  
   Create a file called `webpack.config.js` in your project's root directory:
   ```js
   const path = require('path');
   const { CleanWebpackPlugin } = require('clean-webpack-plugin');
   const TerserPlugin = require('terser-webpack-plugin');

   module.exports = {
       entry: './static/js/index.js',
       output: {
           path: path.resolve(__dirname, 'dist'),
           filename: 'bundle.js',
       },
       mode: 'production',
       module: {
           rules: [
               {
                   test: /\.js$/,
                   exclude: /node_modules/,
                   use: {
                       loader: 'babel-loader',
                       options: {
                           presets: ['@babel/preset-env'],
                       },
                   },
               },
           ],
       },
       optimization: {
           minimize: true,
           minimizer: [new TerserPlugin()],
       },
       plugins: [new CleanWebpackPlugin()],
   };
   ```

3. **Configure Babel (`.babelrc`)**  
   Create a `.babelrc` file:
   ```json
   {
       "presets": ["@babel/preset-env"]
   }
   ```

4. **Modify Flask to Serve Bundled JS**  
   Update your Flask template to reference the bundled file:
   ```html
   <script src="{{ url_for('static', filename='dist/bundle.js') }}"></script>
   ```

5. **Run Webpack**  
   To transpile and bundle your JavaScript files, run:
   ```sh
   npx webpack
   ```

### Explanation:
- `babel-loader` transpiles ES6+ code.
- `TerserPlugin` minifies the code.
- `CleanWebpackPlugin` ensures the `dist/` directory is cleared before each build.
- The output will store the bundled and minified JS file in `dist/`.

Now, Flask can serve the optimized JavaScript file efficiently. Would you like help integrating additional tools like SCSS or TypeScript? [[0]](https://github.com/japb1998/budgetTracker/tree/13130ec2b37b817e9fa97cad2fff6618a98348f3/public/webpack.config.js) [[1]](https://github.com/AmericanPublicPowerAssociation/asset-report-risks/tree/8be299b2fea8133572795d845cb37b756151626c/client/webpack.config.js) [[2]](https://github.com/wilsson/create-webpack-application/tree/0cc8e553fdcb909c88c2e37790d2fa1231c4c8f2/templates/webpack-babel/webpack.config.js) [[3]](https://github.com/jefersonvinicius/js-tdd-course/tree/6f3daf930ac9013f32701c8508b0f5ffaef6eda4/03-js-modules/webpack.config.js) [[4]](https://github.com/igorega/testChess.github.io/tree/5485388ac52027a4634c4efd7c8aa37a820575f2/webpack.config.js)



> [0] [](https://github.com/japb1998/budgetTracker/tree/13130ec2b37b817e9fa97cad2fff6618a98348f3/public/webpack.config.js)
>
> [1] [](https://github.com/AmericanPublicPowerAssociation/asset-report-risks/tree/8be299b2fea8133572795d845cb37b756151626c/client/webpack.config.js)
>
> [2] [](https://github.com/wilsson/create-webpack-application/tree/0cc8e553fdcb909c88c2e37790d2fa1231c4c8f2/templates/webpack-babel/webpack.config.js)
>
> [3] [](https://github.com/jefersonvinicius/js-tdd-course/tree/6f3daf930ac9013f32701c8508b0f5ffaef6eda4/03-js-modules/webpack.config.js)
>
> [4] [](https://github.com/igorega/testChess.github.io/tree/5485388ac52027a4634c4efd7c8aa37a820575f2/webpack.config.js)