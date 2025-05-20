Certainly! Here's a professional CSS animation class you can add to a button used for submitting a form. This example uses a subtle "loading" or "processing" animation to indicate that the form submission is in progress.

### Example: Submit Button with Loading Animation

```css
/* Base button styles (optional) */
.btn-submit {
  padding: 0.75em 1.5em;
  font-size: 1rem;
  color: #fff;
  background-color: #007bff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.3s ease;
}

/* Hover state */
.btn-submit:hover {
  background-color: #0069d9;
}

/* Animation for loading indicator */
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* Loader styles */
.btn-submit.loading {
  cursor: not-allowed;
  opacity: 0.8;
}

/* Adding a spinner inside the button during loading */
.btn-submit.loading::after {
  content: "";
  border: 3px solid rgba(255, 255, 255, 0.3);
  border-top: 3px solid #fff;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  margin-left: 10px;
  animation: spin 1s linear infinite;
}
```

### Usage in HTML and JavaScript:

```html
<button type="submit" class="btn-submit" id="submitBtn">Submit</button>

<script>
  const form = document.querySelector('form'); // assuming you have a form
  const submitBtn = document.getElementById('submitBtn');

  form.addEventListener('submit', function(e) {
    e.preventDefault();

    // Add loading class
    submitBtn.classList.add('loading');
    submitBtn.disabled = true;

    // Simulate form submission process
    setTimeout(() => {
      // Remove loading state after process (e.g., after AJAX call)
      submitBtn.classList.remove('loading');
      submitBtn.disabled = false;

      // Optionally, submit form
      // form.submit();
    }, 3000); // simulate 3 seconds delay
  });
</script>
```

---

### Summary:
- The `.btn-submit` class styles the button.
- The `.loading` class adds a spinner next to the button text using a pseudo-element `::after`.
- The spinner uses CSS animations (`@keyframes spin`) for rotation.
- JavaScript toggles the class on form submission to indicate the loading state.

This approach provides a clean, responsive, and professional user experience during form submission.