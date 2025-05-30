To configure Babel to compile your module located at `static/js/index.js` and output it to `dist/index.js`, you need to follow these steps:

1. **Install Babel and necessary presets/plugins**: If you haven't already, you need to install Babel and any presets or plugins you want to use. You can do this using npm or yarn. For example, to install Babel CLI and the preset for ES2015, you can run:

   ```bash
   npm install --save-dev @babel/core @babel/cli @babel/preset-env
   ```

2. **Create a Babel configuration file**: You can create a `.babelrc` file in the root of your project to specify the presets and plugins you want to use. Here’s a simple example of a `.babelrc` file:

   ```json
   {
     "presets": ["@babel/preset-env"]
   }
   ```

3. **Add a build script to your `package.json`**: You can add a script to your `package.json` to run Babel. Here’s how you can do it:

   ```json
   {
     "scripts": {
       "build": "babel static/js/index.js --out-file dist/index.js"
     }
   }
   ```

4. **Run the build script**: Now you can run the build script using npm or yarn:

   ```bash
   npm run build
   ```

This will compile your module from `static/js/index.js` and output it to `dist/index.js`.

### Summary of Files

- **.babelrc**:
  ```json
  {
    "presets": ["@babel/preset-env"]
  }
  ```

- **package.json** (snippet):
  ```json
  {
    "scripts": {
      "build": "babel static/js/index.js --out-file dist/index.js"
    }
  }
  ```

### Additional Notes

- If you have multiple files to compile or want to compile an entire directory, you can adjust the Babel command accordingly.
- Make sure that the `dist` directory exists or Babel will throw an error. You can create it manually or use a build tool to handle that for you.