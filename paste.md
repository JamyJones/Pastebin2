Certainly! Here's a professional CSS animation class you can add to a Bootstrap button to give it a polished animated effect when clicked or in a loading state, commonly used for submitting forms.

### Example: Loading Spinner Animation on Button

This class creates a loading spinner that appears when the button is in a loading state, providing visual feedback during form submission.

#### 1. CSS Animation Classes

```css
/* Keyframes for spinning animation */
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* Loader styles */
.btn-loading {
  position: relative;
  pointer-events: none; /* Disable click during loading */
  opacity: 0.6;         /* Slightly fade the button to indicate disabled state */
}

/* Spinner element inside button */
.btn-loading::after {
  content: "";
  display: inline-block;
  margin-left: 8px; /* Space between text and spinner */
  width: 16px;
  height: 16px;
  border: 2px solid #fff;
  border-top-color: transparent;
  border-radius: 50%;
  vertical-align: middle;
  animation: spin 0.8s linear infinite;
}
```

#### 2. Usage in HTML

Apply the `btn-loading` class dynamically via JavaScript when form is submitting.

```html
<button id="submitBtn" type="submit" class="btn btn-primary">
  Submit
</button>
```

#### 3. JavaScript to toggle loading state

```js
const submitBtn = document.getElementById('submitBtn');

submitBtn.addEventListener('click', function() {
  // Add loading class
  this.classList.add('btn-loading');
  
  // Disable the button to prevent multiple submits
  this.disabled = true;
  
  // Simulate form submission (replace with your AJAX/blocking call)
  setTimeout(() => {
    // Remove loading class after submission completes
    this.classList.remove('btn-loading');
    this.disabled = false;
  }, 3000); // simulate 3 seconds delay
});
```

---

### Summary
- The `@keyframes spin` creates a continuous rotation.
- The `.btn-loading` class disables the button and adds a spinning indicator after the button text.
- You can toggle this class dynamically during form processing.

### Notes:
- Adjust the size of the spinner (`width`, `height`) and border color as needed.
- For accessibility, consider adding `aria-busy` attributes or visually hidden text indicating a loading state.

Would you like a more advanced animation or a different effect?