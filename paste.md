## How to override Bootstrap form submit button listeners<br>
---<br>
Explanation: When you use Bootstrap, it often relies on JavaScript for certain behaviors, and form submit buttons may have default event listeners attached, especially if you're using Bootstrap's JavaScript components or plugins. Overriding or adding your own listeners requires understanding how event propagation works in JavaScript, as well as managing event listeners properly to prevent conflicts or multiple triggers.<br>

---<br>
**Standard Approach to Override Bootstrap Button Listeners**<br>

### 1. Remove Existing Event Listeners<br>
- First, identify if the existing listeners are attached via JavaScript that you have access to or through Bootstrap's internal scripts.<br>
- Use JavaScript's `removeEventListener()` method to detach specific event handlers if you have references to those functions.<br>
- If you do not have direct references, you can clear event listeners by replacing the button's `onclick` attribute or resetting event bindings.<br>
- Alternatively, **use event delegation** with event `.stopImmediatePropagation()` to prevent other handlers from firing.<br>

### 2. Adding Your Custom Event Listener<br>
- Use `addEventListener()` to attach your own listener to the button.<br>
- Example: <br>
```javascript
const submitBtn = document.querySelector('#yourButtonId');
submitBtn.addEventListener('click', function(event) {
  event.preventDefault(); // prevent default form submission
  // Your custom code here
});
```

### 3. Prevent Default Bootstrap Behavior<br>
- Use `event.preventDefault()` in your handler if you want to stop Bootstrap or other scripts from performing their default submission action.<br>
- Make sure your script runs **after** Bootstrap's scripts load.<br>

### 4. Use Event Delegation for Dynamic Elements<br>
- If buttons are added dynamically, attach listeners to a parent element to control all child buttons.<br>
```javascript
document.querySelector('#parentElement').addEventListener('click', function(e){
    if(e.target && e.target.matches('button#yourButtonId')){
        e.preventDefault();
        // Your override code
    }
});
```

---<br>
**Example**: Overriding Bootstrap button listener<br>
```html
<form id="myForm">
  <button type="submit" id="customBtn" class="btn btn-primary">Submit</button>
</form>
<script>
  // Remove default or existing Bootstrap listeners (if accessible)
  const button = document.getElementById('customBtn');

  // Remove all existing event listeners (if any were attached via addEventListener)
  // Note: JavaScript doesn't provide a way to remove anonymous handlers; you must keep references
  // For this case, override by adding a new listener
  button.addEventListener('click', function(e) {
    e.preventDefault(); // Prevent existing submission
    // Your custom code
    alert('Custom submit logic');
  });
</script>
```

---<br>
**References**:## 
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Events#Event_listeners
- https://getbootstrap.com/docs/5.0/getting-started/javascript/#event-handling