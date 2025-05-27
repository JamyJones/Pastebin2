In JavaScript modules, you can ensure that events are attached after everything is loaded by using the `DOMContentLoaded` event or by placing your script at the end of the body. Here are two common approaches:

### 1. Using `DOMContentLoaded`

You can listen for the `DOMContentLoaded` event, which fires when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading.

```javascript
document.addEventListener('DOMContentLoaded', () => {
    // Your code to attach events goes here
    const button = document.getElementById('myButton');
    button.addEventListener('click', () => {
        console.log('Button clicked!');
    });
});
```

### 2. Placing the Script at the End of the Body

Another approach is to place your script tag just before the closing `</body>` tag. This ensures that the DOM is fully loaded before your script runs.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button id="myButton">Click Me</button>

    <script type="module">
        const button = document.getElementById('myButton');
        button.addEventListener('click', () => {
            console.log('Button clicked!');
        });
    </script>
</body>
</html>
```

### Summary

Both methods ensure that your event listeners are attached after the DOM is fully loaded. The first method is more flexible and can be used in any part of your JavaScript code, while the second method is simpler for small scripts. Choose the one that best fits your needs!