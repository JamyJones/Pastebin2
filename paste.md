To check whether all DOM elements have been created, you can use the `DOMContentLoaded` event in JavaScript. This event is fired when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading. Here's how you can do it:

```javascript
document.addEventListener("DOMContentLoaded", function() {
    // All DOM elements are now available for manipulation
    console.log("All DOM elements have been created.");
    // You can now safely access and manipulate DOM elements here
});
```

If you want to ensure that all resources (like images and stylesheets) are fully loaded, you can use the `load` event on the `window` object:

```javascript
window.addEventListener("load", function() {
    // All DOM elements and resources are fully loaded
    console.log("All DOM elements and resources have been loaded.");
});
```

### Summary:
- Use `DOMContentLoaded` for when the DOM is fully constructed.
- Use `load` for when all resources are fully loaded.