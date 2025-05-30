To configure Babel to compile your JSX module located at `static/js/index.js` and output it to `dist/index.js`, you will need to create a Babel configuration file. The most common way to do this is by using a `.babelrc` file or a `babel.config.js` file. Below is an example of a `babel.config.js` file that you can use:

```javascript
// babel.config.js
module.exports = {
  presets: [
    '@babel/preset-env', // Transpile modern JavaScript
    '@babel/preset-react' // Transpile JSX
  ],
  plugins: [
    // Add any additional plugins here if needed
  ]
};
```

Next, you will need to set up a build script in your `package.json` to compile the JSX file. Here’s how you can do that:

```json
{
  "scripts": {
    "build": "babel static/js/index.js --out-file dist/index.js"
  },
  "devDependencies": {
    "@babel/cli": "^7.x.x", // Replace with the latest version
    "@babel/preset-env": "^7.x.x", // Replace with the latest version
    "@babel/preset-react": "^7.x.x" // Replace with the latest version
  }
}
```

### Steps to Set Up

1. **Install Babel and Presets**: Run the following command to install Babel and the necessary presets:

   ```bash
   npm install --save-dev @babel/cli @babel/preset-env @babel/preset-react
   ```

2. **Create Configuration File**: Create a file named `babel.config.js` in the root of your project and add the configuration provided above.

3. **Add Build Script**: Add the build script to your `package.json` as shown above.

4. **Run the Build**: You can now compile your JSX file by running:

   ```bash
   npm run build
   ```

This will take the `static/js/index.js` file, compile it using Babel, and output the result to `dist/index.js`. Make sure that the `dist` directory exists or Babel will throw an error. You can create it manually or add a script to create it automatically before the build step.