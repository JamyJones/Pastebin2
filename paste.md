When working with React in Vim, the most common file extension is `.jsx`. This extension indicates that the file contains JavaScript with JSX syntax, which is essential for React components.

### Typical file extensions for React development:

- `.jsx` — For React components written with JSX syntax. Many developers prefer using `.jsx` to enable better syntax highlighting and tooling support.
- `.js` — Also widely used, especially if your editor/configuration supports JSX inside `.js` files (via Babel or other preprocessors).
- `.tsx` — If you're using TypeScript with React, then `.tsx` is the appropriate extension.

### Best Practice:
- Use `.jsx` for files containing JSX when working with plain JavaScript.
- Use `.tsx` for TypeScript files with JSX.
- Ensure your Vim environment is configured to recognize these extensions, so syntax highlighting and language features work correctly.

### Additional tips:
- Use appropriate Vim plugins for React development, such as:
  - `vim-jsx`
  - `emmet-vim`
  - `coc.nvim` with `coc-tsserver` or `coc-eslint`

### Example:
Create your component file as `MyComponent.jsx`

```jsx
// MyComponent.jsx
import React from 'react';

function MyComponent() {
  return <div>Hello, React!</div>;
}

export default MyComponent;
```

### Summary:
- Use `.jsx` for React components using JSX syntax.
- For TypeScript + React, use `.tsx`.
- Make sure your Vim setup supports syntax highlighting for these extensions for an optimal development experience.