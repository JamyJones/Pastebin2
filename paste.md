To attach your own listener that triggers *only* when all the Bootstrap form validations pass (i.e., the form is valid), you should:
- Check for validity using `form.checkValidity()`.
- If valid, call your custom logic or listener.
- Prevent form submission when invalid.

Here's a professional way to structure this, including attaching your custom callback:

```js
var forms = document.getElementsByClassName('needs-validation');

Array.prototype.filter.call(forms, function(form) {
  form.addEventListener('submit', function(event) {
    if (form.checkValidity() === false) {
      event.preventDefault();
      event.stopPropagation();
      // Mark form as validated (Bootstrap styling)
      form.classList.add('was-validated');
    } else {
      // Form is valid, perform your custom logic
      event.preventDefault(); // Optional: prevent default if you handle submission via JS
      form.classList.add('was-validated');

      // Call your custom listener/function
      onFormValid(form);
    }
  }, false);
});

// Your custom validation success handler
function onFormValid(form) {
  // Example: console log or initiate AJAX submission
  console.log('Form is valid! Triggering custom behavior.');

  // Example AJAX submission (if needed)
  // submitFormViaAjax(form);
}
```

### Key points:
- When the form checks as `checkValidity() === true`, the form is valid.
- At this point, you invoke your custom listener or function (`onFormValid`).
- Make sure `event.preventDefault()` is called if you are handling the submission via JavaScript (prevent the default submit behavior).

### Additional Tips:
- You might also want to disable the native submit button once the form is valid, or handle the actual data submission via AJAX.
- To improve code separation, you can encapsulate the validation logic and listener attachment in separate functions.
- Remember to adjust for accessibility and progressive enhancement when manipulating form behaviors.

Let me know if you'd like a more complex example involving AJAX, or form reset, etc.