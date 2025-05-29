To configure Webpack so that you can use absolute import paths relative to a specific root directory (like `/static/js/foo.js`), you should:

1. Define a custom **resolve.alias** or **resolve.modules** in your Webpack configuration.  
2. Use the **resolve.modules** option to specify an absolute directory that Webpack will resolve modules from.
3. Or, set up **alias** that points to your desired root directory.

### Recommended Approach: Using `resolve.modules`

This approach allows you to specify a root folder that Webpack will resolve modules from, making imports like `import foo from 'js/foo.js'` possible if `js` is inside the specified directory.

---

### Example:

Suppose your project structure is:

```
project/
│
├── src/
│   ├── static/
│   │   └── js/
│   │       └── foo.js
│   └── index.js
├── webpack.config.js
└── ...
```

You want to import `foo.js` in your code with an absolute path like `/static/js/foo.js`.

---

### Webpack configuration:

```js
const path = require('path');

module.exports = {
  // ... other configurations
  resolve: {
    modules: [
      path.resolve(__dirname, 'src'), // Add src as root for modules
      'node_modules' // fallback
    ],
    // Prevents needing to specify relative paths for modules inside 'src'
  },
  // Optionally, you can also create aliases
  // resolve: {
  //   alias: {
  //     static: path.resolve(__dirname, 'src/static')
  //   }
  // }
};
```

### Usage in your code:

```js
import foo from 'static/js/foo.js';
```

Notice that with this setup, you do **not** need to specify relative paths like `'../../...'`.

---

### Alternative: Using `resolve.alias`

If you want to map `/static` to a specific directory:

```js
resolve: {
  alias: {
    '/static': path.resolve(__dirname, 'src/static')
  }
}
```

Then you can do:

```js
import foo from '/static/js/foo.js';
```

---

### Additional Tips:

- Webpack does not support import paths starting with `/` as root in the import statement by default. The above methods are ways to emulate this behavior.
- For local development, it's common to use relative paths, but aliasing improves readability and maintainability, especially in large projects.
- In server-side code, ensure you also properly resolve absolute paths with `path.resolve()`.

---

### Summary:

- Use `resolve.modules` to include your project root directory.
- Or use `resolve.alias` to create custom root paths.
- Remember to adjust your import statements to match your configuration.

---

If you want me to prepare a full sample `webpack.config.js` or provide instructions for a specific project structure, let me know!