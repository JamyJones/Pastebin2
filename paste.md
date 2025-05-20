## Overriding Bootstrap Form Submit Button Listeners

---

**Summary:**  
You want to override or replace the default event listeners attached to a Bootstrap form submit button.

---

**Explanation:**  

### Default Behavior of Bootstrap Buttons and Form Submission  
Bootstrap itself is primarily a front-end framework that styles HTML elements like buttons and forms. It does **not** attach any JavaScript event listeners for form submission by itself. Instead, if you see event handlers attached, they are either by Bootstrap plugins or custom scripts in your project.

### How to override existing event listeners

**1. Remove existing event listeners**  
- Use **JavaScript** to remove specific event listeners attached to the button or form.
- If the listener was added via `addEventListener`, you can remove it using `removeEventListener`, but you need to have a reference to the function attached.

```js
// Example: Remove a specific event listener
const button = document.querySelector('#myButton');

function handleClick(event) {
    // existing handler code
}

// Attach
button.addEventListener('click', handleClick);

// Remove
button.removeEventListener('click', handleClick);
```

*Note:* If the event was attached inline in HTML (e.g., `<button onclick="...">`), you cannot remove it via JS and need to override by overwriting the inline attribute.

**2. Override using event delegation or re-bind event**  
- Use **JavaScript** to add a new event listener, which takes precedence because multiple handlers can be attached to the same element.

```js
// Override previous handler by adding a new one
button.addEventListener('click', function(event) {
    event.preventDefault(); // prevent default form submission
    // your custom code here
});
```

This way, your new handler runs after the previous if not removed, and the call to `preventDefault()` stops the form from submitting.

**3. Prevent default form submission directly**  
- A common approach involves intercepting the form's submit event.

```js
const form = document.querySelector('#myForm');

form.addEventListener('submit', function(event) {
    event.preventDefault(); // stops the default submission
    // new custom submit logic
});
```

This is **more reliable** for overriding form submission behaviors.

---

**Example: Custom Submission Handler**  

```js
// Select form element
const myForm = document.querySelector('#myForm');
  
// Attach your custom submit handler
myForm.addEventListener('submit', function(e) {
    e.preventDefault(); // prevent Bootstrap or default behavior
    alert('Custom submission logic here!');
    // Perform validation, AJAX, etc.
});
```

---

### Summary of best practices:

- To **completely override existing handlers**, remove them with `removeEventListener()`, if possible.
- **Intercept form submission** directly with the `submit` event.
- Use `event.preventDefault()` within your handler to **stop default submission**.
- Add your **custom logic** after preventing the default.

---

**References:**  
##https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener##  
##https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener##  
##https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit##