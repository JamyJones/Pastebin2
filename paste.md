To configure Babel to compile your module from `static/js/index.js` to `dist/index.js`, follow these steps:

### 1. Install Babel and Required Packages
First, ensure you have Babel installed in your project along with the necessary presets:

```sh
npm install --save-dev @babel/core @babel/cli @babel/preset-env
```

### 2. Create a Babel Configuration File
In your project's root directory, create a `.babelrc` configuration file and add the following settings:

```json
{
  "presets": ["@babel/preset-env"]
}
```

This configures Babel to use `@babel/preset-env`, which allows you to compile modern JavaScript down to a version that is compatible with older browsers or environments.

### 3. Run Babel CLI to Compile Your Code
You can now use Babel CLI to transpile your module. Run the following command:

```sh
npx babel static/js/index.js --out-file dist/index.js
```

This instructs Babel to take `static/js/index.js` as the input and output the compiled JavaScript to `dist/index.js`.

### 4. Automate the Process with npm Scripts
To streamline the process, add an npm script in your `package.json`:

```json
{
  "scripts": {
    "build": "babel static/js/index.js --out-file dist/index.js"
  }
}
```

Now you can compile your module simply by running:

```sh
npm run build
```

### Best Practices
- **Use `.babelrc` or `babel.config.json` for scalability**: Keeping configurations separate helps maintain clean code.
- **Enable source maps** for better debugging: You can add the `--source-maps` flag to your Babel CLI command.
- **Consider using Babel with Webpack** if your project requires bundling multiple modules.

Would you like help integrating Babel with Webpack or setting up additional features like polyfills?