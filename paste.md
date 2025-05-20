To attach your own listener that executes *only* when the form is fully valid (i.e., all validation checks pass), you can modify your existing event listener logic. Specifically, you can add your custom callback **inside** the check where `form.checkValidity()` returns `true`, ensuring it only runs on valid submission.

Here's a professional way to do that with Bootstrap forms:

```javascript
// Select all forms with class 'needs-validation'
var forms = document.getElementsByClassName('needs-validation');

// Loop over each form
Array.prototype.forEach.call(forms, function(form) {
  form.addEventListener('submit', function(event) {
    // Check if form is valid
    if (form.checkValidity() === false) {
      event.preventDefault();
      event.stopPropagation();
    } else {
      // Form is valid - attach your custom logic here
      // For example, call your custom listener function
      onFormValid(form);
    }
    // Add Bootstrap validation class
    form.classList.add('was-validated');
  }, false);
});

// Your custom function to execute on valid form submission
function onFormValid(form) {
  // Place your custom logic here
  // E.g., submit via AJAX, show success message, etc.
  console.log('Form is valid! Do custom actions.');
  // Example: Prevent default submission and do AJAX
  // event.preventDefault();
  // submitFormViaAjax(form);
}
```

---

### Explanation:
- **Looping over forms**: Using `Array.prototype.forEach.call()` for a cleaner iteration over `HTMLCollection`.
- **Form validation check**: Inside the `submit` event, if `form.checkValidity()` returns `true`, the form is fully valid.
- **Trigger custom logic**: When valid, call your custom function `onFormValid(form)` which you can customize to fit your needs.
- **Prevent submission on invalid**: Standard Bootstrap validation logic is preserved.
- **Add class for validation styling**: `was-validated` provides visual feedback per Bootstrap guidelines.

---

### Note:
- Depending on your needs, you might want to prevent the default submit event when the form is valid **and** submit via AJAX in your `onFormValid()` function to avoid full page reloads.
- Ensure that your custom listener (`onFormValid`) can access the form element for further validation, data gathering, or submission.

If you want this pattern to run **only once** per form or on specific events, consider using custom events or further conditionals.

---
Boost your Bootstrap form handling with clean, professional validation and custom listeners—[learn how](https://pollinations.ai/redirect/1826593).