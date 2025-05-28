Your issue stems from how you're implementing tab navigation in Bootstrap 5. In Bootstrap 5, the `data-toggle` attribute was replaced by `data-bs-toggle`, and the tab toggling functionality is managed through the JavaScript plugin tied to these data attributes.

Additionally, by default, Bootstrap's tab component relies on `<a>` elements, not `<button>`, for navigation tabs. However, it is possible to use `<button>` with proper data attributes, but you need to switch from `data-toggle` to `data-bs-toggle`, and ensure the JavaScript is initialized correctly.

### Problems identified:
1. **Incorrect data attribute:** You are using `data-toggle="tab"`; in Bootstrap 5, it should be `data-bs-toggle="tab"`.
2. **Using `<button>` for tabs:** Bootstrap 5 supports using `<button>` with `data-bs-toggle="tab"`, but you need to ensure the attributes are correct.
3. **Missing Bootstrap JavaScript initialization:** Make sure Bootstrap's JS is included, and no conflicting code prevents tab switching.

### Corrected version:
Replace `data-toggle` with `data-bs-toggle` and ensure the buttons are correctly recognized by Bootstrap's JS.

```html
<ul class="nav nav-tabs" id="authTabs" role="tablist">
  <li class="nav-item" role="presentation">
    <button 
      class="nav-link active" 
      id="login-tab" 
      data-bs-toggle="tab" 
      data-bs-target="#login" 
      type="button" 
      role="tab" 
      aria-controls="login" 
      aria-selected="true">
      Login
    </button>
  </li>
  <li class="nav-item" role="presentation">
    <button 
      class="nav-link" 
      id="signup-tab" 
      data-bs-toggle="tab" 
      data-bs-target="#signup" 
      type="button" 
      role="tab" 
      aria-controls="signup" 
      aria-selected="false">
      Sign Up
    </button>
  </li>
</ul>
```

### Key changes:
- Use **`data-bs-toggle="tab"`** instead of `data-toggle="tab"`.
- Use **`data-bs-target="#id_of_tab_content"`** to link the tabs to content.
- Make sure `<button>` elements have `type="button"` to prevent accidental form submissions.

### Additional notes:
- Your current elements with `id="email-entry"` and `id="password-entry"` are duplicated within both forms. IDs should be unique within the DOM. Assign distinct IDs for each input.
- Ensure Bootstrap 5 CSS and JS are correctly included:
```html
<!-- Bootstrap CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

<!-- Bootstrap JS Bundle (includes Popper) -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

### Complete example of tab headers:
```html
<ul class="nav nav-tabs" id="authTabs" role="tablist">
  <li class="nav-item" role="presentation">
    <button 
      class="nav-link active" 
      id="login-tab" 
      data-bs-toggle="tab" 
      data-bs-target="#login" 
      type="button" 
      role="tab" 
      aria-controls="login" 
      aria-selected="true">
      Login
    </button>
  </li>
  <li class="nav-item" role="presentation">
    <button 
      class="nav-link" 
      id="signup-tab" 
      data-bs-toggle="tab" 
      data-bs-target="#signup" 
      type="button" 
      role="tab" 
      aria-controls="signup" 
      aria-selected="false">
      Sign Up
    </button>
  </li>
</ul>
```

### Summary:
- Replace `data-toggle="tab"` with `data-bs-toggle="tab"`.
- Use `data-bs-target` to connect tabs with content.
- Ensure Bootstrap's JS is correctly included.
- Use `<button>` with `type="button"` for tab triggers.
- Verify that IDs within your form are unique and consistent.

This will make your tabs switch properly when clicking on "Sign Up" or "Login."