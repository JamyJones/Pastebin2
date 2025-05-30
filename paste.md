Certainly! Below is a complete Babel configuration file (`babel.config.js`) to compile your JSX module located at `static/js/index.js` and output it to `dist/index.js`.

### Overview:
- You will typically use Babel with a build tool (like Webpack, Rollup, or a simple script) to specify input and output files.
- Babel itself primarily provides the transformation configuration, while file management (reading input and writing output) is handled by the build tool or a custom script.

### Step 1: Babel Configuration (`babel.config.js`)
This configuration will specify the presets (like `@babel/preset-env` and `@babel/preset-react`) needed to handle modern JavaScript and JSX syntax.

```js
// babel.config.js
module.exports = {
  presets: [
    '@babel/preset-env',  // For transforming modern JavaScript into compatible syntax
    '@babel/preset-react' // For transforming JSX syntax
  ],
};
```

### Step 2: Compilation Script
Since Babel itself does not handle file I/O, you can use a Node.js script or CLI command to compile your specific file.

Here's a simple example using the Babel CLI:

```bash
npx babel static/js/index.js --out-file dist/index.js
```

### Optional: Automating with an NPM Script
Add this to your `package.json`:

```json
{
  "scripts": {
    "build": "babel static/js/index.js --out-file dist/index.js"
  }
}
```

Then run:

```bash
npm run build
```

### Summary
- **Babel config (`babel.config.js`)**: Defines how JSX and modern JS are transformed.
- **Build command**: Specifies input and output files, enabling you to compile your module correctly.

---

### Complete example:

**`babel.config.js`**
```js
module.exports = {
  presets: [
    '@babel/preset-env',
    '@babel/preset-react'
  ],
};
```

**Build command (CLI)**:
```bash
npx babel static/js/index.js --out-file dist/index.js
```

Or via `package.json` script:
```json
"scripts": {
  "build": "babel static/js/index.js --out-file dist/index.js"
}
```

This setup ensures your JSX code is correctly transpiled, and outputted to the desired location.