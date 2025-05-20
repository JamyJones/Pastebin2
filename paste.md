To attach your own listener that executes **only** when the form is valid (i.e., all validation passes), you should listen for the `submit` event, check validity, and then invoke your custom handler if the form is valid.

Here's a professional approach:

### Step-by-step guide:

1. **Listen for the `submit` event** on the form.
2. **Prevent submission** if invalid.
3. **When the form is valid**, call your custom logic after validation passes.

### Example implementation:

```js
// Fetch all forms with the class 'needs-validation'
var forms = document.getElementsByClassName('needs-validation');

Array.prototype.forEach.call(forms, function(form) {
  form.addEventListener('submit', function(event) {
    // Check if the form is valid
    if (form.checkValidity() === false) {
      event.preventDefault(); // Prevent form submission
      event.stopPropagation();
      // Add bootstrap validation feedback
      form.classList.add('was-validated');
    } else {
      // Form is valid, attach your custom handler here
      event.preventDefault(); // Optional: prevent default to handle form via AJAX
      form.classList.add('was-validated');

      // Call your custom function for valid form submission
      handleValidForm(form);
    }
  }, false);
});

// Define your custom handler
function handleValidForm(form) {
  // Your custom logic here, for example:
  // - Submit via AJAX
  // - Display a success message
  // - Reset the form
  console.log('Form is valid, processing form...');
  
  // Example: Submitting via Fetch API
  const formData = new FormData(form);
  
  fetch('/submit-endpoint', {
    method: 'POST',
    body: formData
  })
  .then(response => response.json())
  .then(data => {
    // Handle server response
    console.log('Success:', data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
}
```

### Key points:
- `event.preventDefault()` prevents the browser's default form submission unless the form is valid.
- Once the form passes validation, you can execute **any custom logic** in `handleValidForm`.
- This approach adheres to accessibility and Bootstrap's validation styling.

---

**Optional enhancement:**  
If you want the form to be submitted normally when valid, remove the `event.preventDefault()`, and only run your custom logic before submission.

Let me know if you'd like an example involving AJAX form submission, file uploads, or other advanced techniques!