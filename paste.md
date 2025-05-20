Certainly! Here's a professional CSS animation class that you can add to a button to give it a sleek, attention-grabbing effect during form submission.

### Example: Button Submission Loading Animation

This example creates a pulsating effect to indicate the form is being submitted.

```css
/* Define keyframes for the pulsating effect */
@keyframes pulse {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.05);
    opacity: 0.7;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

/* Animation class for the button */
.btn-submit-loading {
  position: relative;
  overflow: hidden;
  cursor: not-allowed; /* Change cursor to indicate disabled state */
  animation: pulse 1s infinite; /* Apply pulsate animation infinitely */
  opacity: 0.8; /* Slightly reduce opacity for disabled aesthetic */
}

/* Optional: Add a spinner inside the button for better UX */
.btn-submit-loading::after {
  content: "";
  display: inline-block;
  width: 16px;
  height: 16px;
  margin-left: 8px;
  border: 2px solid #fff;
  border-top-color: transparent;
  border-radius: 50%;
  vertical-align: middle;
  animation: spin 0.8s linear infinite;
}

/* Define spin keyframes for spinner */
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```

### Usage:

```html
<button id="submitBtn" class="btn">Submit</button>
```

### JavaScript to toggle the loading class:

```js
const button = document.getElementById('submitBtn');

button.addEventListener('click', () => {
  // Add loading class when submitting the form
  button.classList.add('btn-submit-loading');

  // Simulate async submission (replace with your actual form submission logic)
  setTimeout(() => {
    // Remove loading class after submission completes
    button.classList.remove('btn-submit-loading');
  }, 3000); // 3 seconds delay
});
```

### Summary:
- The `.btn-submit-loading` class applies a pulsating animation.
- An optional spinner is added via `::after` pseudo-element to improve UX.
- The class can be toggled during form submission to provide visual feedback.

Feel free to customize the colors, animation duration, or add other animations as needed!