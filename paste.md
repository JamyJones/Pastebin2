## How to Override Bootstrap's Form Submit Button Listeners

---

**Summary:**  
You want to replace or extend the default event handlers attached to a Bootstrap form submit button, which are typically added via JavaScript or HTML attributes.

---

### Explanation

**Bootstrap's form submit button default behavior:**  
Bootstrap itself does not automatically attach JavaScript event listeners to form submit buttons; instead, it relies on HTML forms' native submit events and optional custom scripts you or your project might add. If you want to override or remove existing event listeners attached to a submit button, you'll need to work with JavaScript’s event handling methods.

---

### How to override event listeners on a submit button

**Step 1: Remove existing event listeners**

- Use `removeEventListener()` method:  
  For this to work, the event listener must have been added with `addEventListener()`.  
  Example:  
  ```js
  const btn = document.querySelector('#submitBtn');
  btn.removeEventListener('click', originalHandler);
  ```

- **Note:**  
  **`removeEventListener()`** only works if the exact function reference used when attaching the listener is available. You cannot remove anonymous functions.  
  ```js
  // When adding:
  btn.addEventListener('click', handleClick);
  
  // When removing:
  btn.removeEventListener('click', handleClick);
  ```

**Step 2: Override default or existing behavior**

- **Attach a new event listener:**  
  Add your custom listener using `addEventListener()`.  
  Example:  
  ```js
  btn.addEventListener('click', function(e) {
    e.preventDefault(); // Prevent default form submission
    // Your custom code here
  });
  ```

- **Override form submission:**  
  To block the default submission and replace it:  
  ```js
  const form = document.querySelector('#myForm');
  form.addEventListener('submit', function(e) {
    e.preventDefault(); // Stops the default event
    // Custom form validation or actions
  });
  ```

---

### Practical Example

```html
<form id="myForm">
  <input type="text" name="name" required>
  <button type="submit" id="submitBtn" class="btn btn-primary">Submit</button>
</form>
```

```js
// Assume there's a Bootstrap default or custom listener attached previously
const submitBtn = document.querySelector('#submitBtn');

// Remove previous listener if known and accessible
// e.g., if previousListener was stored
// submitBtn.removeEventListener('click', previousListener);

// Or, override with a new handler
submitBtn.addEventListener('click', function(e) {
  e.preventDefault(); // Stop Bootstrap or default behavior
  alert('Custom Submit Handling');
  // You can programmatically submit the form if necessary
  // document.querySelector('#myForm').submit();
});
```

---

### Tips:
- Use **event delegation** on a parent element if multiple buttons or dynamic elements are involved.
- *Always* prevent default form actions if necessary when overriding submission behavior.
- Check whether your handlers are attached through inline HTML (`onclick` attribute), which requires removing or overriding differently.

---

## References:
##https://developer.mozilla.org/en-US/docs/Web/API/EventListener
##https://getbootstrap.com/docs/5.0/forms/validation/