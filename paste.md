To append a new `<script>` tag dynamically to the DOM in JavaScript, the standard approach involves creating a `<script>` element, setting its attributes (such as `src` or inline code), and then appending it to the document’s `<head>` or `<body>`. This can be useful for loading external scripts dynamically or adding inline scripts.

Here's a step-by-step example demonstrating both approaches:

### 1. Append an external script:

```javascript
const script = document.createElement('script');
script.src = 'https://example.com/script.js'; // URL of the external script
script.async = true; // Optional: load asynchronously

// Append to head or body
document.head.appendChild(script);
```

### 2. Append an inline script:

```javascript
const inlineScript = document.createElement('script');
inlineScript.type = 'text/javascript';
inlineScript.textContent = `
  // Your inline JavaScript code here
  console.log('Inline script executed!');
`;

// Append to head or body
document.body.appendChild(inlineScript);
```

### Additional tips:

- **Choosing insertion point**: Append to `<head>` for scripts that initialize before DOM content, or `<body>` if the script interacts with DOM elements that are already loaded.
- **Event handling**: To execute code after the script loads (especially for external scripts), you can add event listeners:

```javascript
script.onload = () => {
  console.log('External script loaded!');
};
```

### Complete Example – Dynamically load an external script:

```javascript
function loadScript(url, callback) {
  const script = document.createElement('script');
  script.src = url;
  script.onload = callback;
  document.head.appendChild(script);
}

// Usage
loadScript('https://example.com/script.js', () => {
  console.log('Script loaded and executed.');
});
```

This pattern ensures proper handling and execution flow, adhering to best practices for dynamic script appending in a professional environment.