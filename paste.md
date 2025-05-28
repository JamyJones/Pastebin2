To show a popover when hovering over a button using Bootstrap, you can utilize Bootstrap's built-in Popover component. Bootstrap's Popovers are based on Popper.js and provide a flexible way to display contextual content.

### Basic steps:
1. Include Bootstrap CSS & JS (with dependencies: Popper.js and Bootstrap JS).
2. Initialize popovers with data attributes or JavaScript.
3. Configure the hover trigger behavior.

---

### Example: Show popover on hover for a button

#### 1. Include Bootstrap CSS & JS (via CDN)

```html
<head>
  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
  <!-- Your content here -->

  <!-- Bootstrap JS bundle (includes Popper) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
```

#### 2. Create the button with data attributes for popover

```html
<button type="button" class="btn btn-primary"
        data-bs-toggle="popover"
        data-bs-content="This is the popover content!"
        data-bs-trigger="hover"
        data-bs-title="Popover Title"
        id="hoverButton">
  Hover over me
</button>
```

#### 3. Initialize the popover with JavaScript

```javascript
<script>
  document.addEventListener('DOMContentLoaded', function () {
    var popoverTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="popover"]'));
    var popoverList = popoverTriggerList.map(function (popoverTriggerEl) {
      return new bootstrap.Popover(popoverTriggerEl, {
        trigger: 'hover', // or 'focus', 'click', 'manual'
        placement: 'top'  // or 'bottom', 'left', 'right'
      });
    });
  });
</script>
```

---

### Key Points:
- `data-bs-toggle="popover"` initializes the popover.
- `data-bs-trigger="hover"` ensures the popover appears on hover.
- The content and title can be customized with `data-bs-content` and `data-bs-title`.
- The JavaScript part initializes all elements with `[data-bs-toggle="popover"]` efficiently and applies the desired options.

---

### Notes:
- Bootstrap 5 uses `data-bs-*` attributes, unlike Bootstrap 4 which uses `data-toggle` and `data-content`.
- To prevent the popover from closing when the mouse hovers over it (e.g., if content is interactive), additional configuration might be necessary.

---

Let me know if you want an example with custom styling or with content loaded dynamically!