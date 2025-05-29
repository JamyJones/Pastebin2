To set a custom root directory for your project so that you can use absolute import paths like `/static/js/foo.js`, you typically configure your Webpack build to resolve modules from a specific directory. This approach allows you to write cleaner import statements without relative paths.

### Approach: Using `resolve.modules` in Webpack

1. **Configure Webpack's `resolve.modules`:**  
   This setting tells Webpack where to look for modules when resolving imports. By default, it includes `'node_modules'`, but you can add your project root or specific folders here.

2. **Use an alias (Optional but recommended):**  
   To define specific base directories or virtual paths, you can use the `resolve.alias` configuration.

---

### Example Webpack Configuration

Suppose your project structure is:

```
/project-root
  /static
    /js
      foo.js
  src
    index.js
  webpack.config.js
```

And you want to be able to import `/static/js/foo.js` with an absolute path.

**webpack.config.js:**

```js
const path = require('path');

module.exports = {
  // Entry point, output, etc.
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },

  resolve: {
    // Add your root directory to the modules search paths
    modules: [
      path.resolve(__dirname),         // Project root
      'node_modules'                   // Default
    ],
    // Optional: create specific aliases
    alias: {
      Static: path.resolve(__dirname, 'static') // Allows import from 'Static/...'
    }
  },

  // rest of your config...
};
```

### Usage in your code:

- **Using resolve.modules:**

```js
import foo from '/static/js/foo.js'; // Will work if 'static' is resolved relative to project root
// Note: Webpack interprets paths starting with '/' relative to the project's resolution paths,
```

- **Using alias:**

```js
import foo from 'Static/js/foo.js';  // From alias 'Static'
```

### Important Notes:

- **Absolute paths with a leading slash (`/`)**:  
  These are traditionally interpreted as root relative URLs in browsers. When used in modules, they often mean absolute from the server root.  
  For bundling, the approach is to configure path resolution and avoid relying on leading `/` in import statements, or customize how your bundler resolves such paths.

- **Better practice:**  
  Instead of using `/static/...`, consider defining aliases or environment variables, e.g.,:

```js
// Using alias
import foo from 'Static/js/foo.js';

// Or with environment variable
import foo from `${process.env.ASSET_PATH}/js/foo.js`;
```

And set `ASSET_PATH` via environment configuration or Webpack's `DefinePlugin`.

---

### Summary
- Use `resolve.modules` to add your project root directory for resolving modules.
- Alternatively, define aliases with `resolve.alias`.
- Refrain from relying on import paths that start with `/` directly; instead, use aliases or relative paths cleaned up by Webpack.

---

If you want an example of handling environment-specific root paths or dynamic resolution, ask!