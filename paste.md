## How to override Bootstrap form submit button listeners

---
Explanation:

**Bootstrap’s default behavior and event listeners**

Bootstrap itself primarily provides styles and some interactive components (like modals, tooltips, etc.), but it doesn't attach default JavaScript event listeners to form submit buttons. Usually, the event listeners attached to form submit buttons are added by developers with custom JavaScript or jQuery code.

**Why override or remove existing event listeners?**

If your form's submit button already has event listeners (such as preventing default action, validation, or Ajax submission), and you want to override these, you'll need to:

1. Remove the existing event listeners
2. Attach new event listeners with the desired behavior

---

### How to override event listeners on a submit button

**Step 1: Identify the event listeners**

Check the existing event listeners attached to your submit button. For example:

```javascript
// Assuming your button has an id 'submitBtn'
$('#submitBtn').on('click', existingFunction);
```

**Step 2: Remove existing event listeners**

You can remove event listeners attached with jQuery using `.off()`:

```javascript
$('#submitBtn').off('click');
```

This will remove all click event listeners from that button. If you want to remove specific handlers, you need to pass the same function reference.

**Note:** If event listeners were attached via vanilla JavaScript, you can remove them with `removeEventListener()`, but you need to have a reference to the original handler.

---

### Attaching your own event listener to override

**Step 3: Add your custom listener**

```javascript
$('#submitBtn').on('click', function(e) {
    e.preventDefault(); // prevent default form submission

    // Your custom code here
    alert('Custom submit logic');
});
```

This will override previous click event handlers if `.off()` was called beforehand.

---

### Intercepting form submission directly

Alternatively, intercept the form's submit event to override all default behaviors:

```javascript
$('form').on('submit', function(e) {
    e.preventDefault();

    // Your custom submit handling
    console.log("Form submission has been overridden");
});
```

**This method is effective because it catches the submit event before the form is sent.**

---

### Summary

- Bootstrap does not directly add submit button listeners; they're added by user scripts.
- To override existing listeners, remove them with `.off()` in jQuery.
- Attach your new event handler using `.on()`.
- You can also intercept the form’s submit event directly for more control.

---
Example:

```html
<form id="myForm">
  <button type="submit" id="submitBtn">Submit</button>
</form>
```

```javascript
// Remove existing listeners on submit button
$('#submitBtn').off('click');

// Add your custom behavior
$('#submitBtn').on('click', function(e) {
  e.preventDefault();
  alert('Handling submission your way!');
});

// Alternatively, handle form submit directly
$('#myForm').on('submit', function(e) {
  e.preventDefault();
  alert('Form overridden and submitted!');
});
```

---
References:

## https://api.jquery.com/off/  
## https://api.jquery.com/on/  
## https://api.jquery.com/submit/