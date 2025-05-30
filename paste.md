To create a standalone bundle containing all React-related dependencies in a single file (`all_react.js`) and place it in the `dist/` directory, you can use Webpack for bundling.

### Steps:
1. Install Webpack and Webpack CLI:
   ```sh
   npm install --save-dev webpack webpack-cli
   ```
2. Create a Webpack configuration file (`webpack.config.js`) at the root of your project:
   ```js
   const path = require('path');

   module.exports = {
     entry: {
       all_react: ['react', 'react-dom']
     },
     output: {
       filename: '[name].js',
       path: path.resolve(__dirname, 'dist'),
     },
     mode: 'production',
   };
   ```
3. Add a Webpack build script to `package.json`:
   ```json
   "scripts": {
     "build-react": "webpack --config webpack.config.js"
   }
   ```
4. Run the build script:
   ```sh
   npm run build-react
   ```

This will generate `dist/all_react.js`, bundling `react` and `react-dom` into a single file that can be used independently.

Let me know if you need adjustments or optimizations! 🚀