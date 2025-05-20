## Customizing Bootstrap Form Submit Button Event Listeners

---

**Explanation:**

**Using JavaScript or jQuery to override default event listeners of a Bootstrap form submit button**.

---

### Understanding the Context

- Bootstrap **does not** add intrinsic event listeners to form submit buttons.
- Typically, **event listeners** are attached **by your JavaScript code** or by third-party libraries.
- If you want to override or remove existing listeners, you need to understand what is attaching them.

### How to override event listeners

---

### Removing existing event listeners

- **Use the `removeEventListener` method** if the listener was added via JavaScript.
  - Example:

```js
const button = document.getElementById('submitBtn');
button.removeEventListener('click', originalHandler);
```

- **Note**: To successfully remove, you must reference the **same function** used during attaching.

---

### Overriding or adding new event listeners

- To **add your own** event handler **that overrides existing behavior**:

```js
// Select the button
const submitBtn = document.querySelector('#submitBtn');

// Remove existing listeners if possible
// (If they were added via JavaScript and accessible)

// Attach your own event listener
submitBtn.addEventListener('click', function(event) {
    event.preventDefault(); // Prevent default submission if needed
    // Your custom code here
});
```

---

### Using **jQuery** (common with Bootstrap projects)

```js
$('#submitBtn').off('click'); // Remove all previous click handlers
$('#submitBtn').on('click', function(e) {
    e.preventDefault(); // Prevent form from submitting
    // Your custom code
});
```

- `.off()` removes previous handlers
- `.on()` attaches **new** event handler

---

### Important notes:

- **Ensure** your script runs **after** the event listeners are attached.
- Place your script **after** the button HTML, or inside a DOMContentLoaded event.
  
---

### Example:

Suppose your HTML:

```html
<form id="myForm">
  <button type="submit" id="submitBtn" class="btn btn-primary">Submit</button>
</form>
```

Your script:

```js
document.addEventListener('DOMContentLoaded', () => {
    const btn = document.getElementById('submitBtn');

    // Remove all existing click event listeners
    btn.replaceWith(btn.cloneNode(true));
    const newBtn = document.getElementById('submitBtn'); // Clone removes listeners

    // Add your custom event
    newBtn.addEventListener('click', (e) => {
        e.preventDefault();
        alert('Custom submit handler');
        // Additional logic
    });
});
```

### Why clone node?
- When you clone an element with `.cloneNode(true)`, all attached event listeners are **removed**.
- Replacing the original with the clone effectively **resets** event listeners.

---

**Summary:**

- Bootstrap doesn't add event listeners to submit buttons by default.
- To override existing listeners, **remove or replace** them using JavaScript/jQuery.
- Use `.removeEventListener()`, `.off()`, or clone the button to clear event handlers.
- Attach your own handlers with `.addEventListener()` or `.on()`.

---

**References:**

## https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener
## https://api.jquery.com/off/
## https://api.jquery.com/on/