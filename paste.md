Certainly! To compile your JSX module located at `"static/js/index.js"` and output to `"dist/index.js"` using Babel, you need to create a Babel configuration file (`babel.config.json` or `babel.config.js`), along with a build script or command to run the compilation.

### 1. Install necessary Babel packages

First, ensure you have the following Babel packages installed:

```bash
npm install --save-dev @babel/core @babel/cli @babel/preset-env @babel/preset-react
```

### 2. Create Babel configuration file

In this example, we'll create a `babel.config.json` file that specifies the presets needed for JSX and modern JavaScript features.

```json
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

### 3. Build command

Now, you can run Babel via CLI to compile your JSX module:

```bash
npx babel static/js/index.js --out-file dist/index.js
```

### 4. Full setup with package.json script (optional but recommended)

To streamline the build process, add a script in your `package.json`:

```json
{
  "scripts": {
    "build": "babel static/js/index.js --out-file dist/index.js"
  }
}
```

Then, run:

```bash
npm run build
```

---

### Summary:
- Create a `babel.config.json` with the following content:

```json
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

- Use the CLI command:

```bash
npx babel static/js/index.js --out-file dist/index.js
```

or via npm script for convenience.

This setup ensures your JSX in `static/js/index.js` is compiled properly to `dist/index.js`.