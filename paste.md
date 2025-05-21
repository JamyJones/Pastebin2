To append a new `<script>` tag to the DOM in JavaScript, you can create a new `<script>` element using `document.createElement`, set its attributes (like `src` for external scripts), and then append it to the desired location in the DOM. Here's an example:

```javascript
// Create a new script element
var script = document.createElement('script');

// Set the source of the script
script.src = 'https://example.com/script.js'; // Replace with your script URL

// Optionally, you can set other attributes
script.type = 'text/javascript'; // Set the type attribute
script.async = true; // Load the script asynchronously

// Append the script to the body or head
document.body.appendChild(script); // or document.head.appendChild(script);
```

In this example, the script will be loaded asynchronously, which is often recommended to avoid blocking the rendering of the page. You can also append the script to the `<head>` section if that suits your needs better.