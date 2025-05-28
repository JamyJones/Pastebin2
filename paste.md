To show a popper (tooltip or popover) on hover over a button in Bootstrap, it's recommended to use Bootstrap's built-in Popover component, which is based on Popper.js. Here's a step-by-step guide with a code example:

### 1. Include Bootstrap CSS and JS
Ensure you have Bootstrap CSS, Bootstrap JS, and Popper.js included in your project.

```html
<!-- Bootstrap CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

<!-- Bootstrap JS bundle includes Popper.js -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

### 2. Create the Button and Popover Element

```html
<button type="button" class="btn btn-primary" id="hoverButton" data-bs-toggle="popover" data-bs-trigger="hover" data-bs-content="This is a popover!">
  Hover me
</button>
```

### 3. Initialize the Popover via JavaScript

Bootstrap 5 uses data attributes for initialization, but for more control or multiple elements, you can initialize via JavaScript:

```js
document.addEventListener('DOMContentLoaded', () => {
  const popoverTrigger = document.getElementById('hoverButton');
  const popover = new bootstrap.Popover(popoverTrigger, {
    trigger: 'hover', // Show on hover
    placement: 'top', // Position of the popover
  });
});
```

### 4. Complete Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Bootstrap Popover on Hover</title>
  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" />
</head>
<body>
  <div class="container my-5 text-center">
    <button type="button" class="btn btn-primary" id="hoverButton" data-bs-toggle="popover" data-bs-content="This is a popover!">
      Hover me
    </button>
  </div>

  <!-- Bootstrap JS Bundle (includes Popper.js) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
  <script>
    // Initialize Popover on hover
    document.addEventListener('DOMContentLoaded', () => {
      const button = document.getElementById('hoverButton');
      new bootstrap.Popover(button, {
        trigger: 'hover',
        placement: 'top',
      });
    });
  </script>
</body>
</html>
```

---

### Key points:
- `trigger: 'hover'` makes the popover appear when hovering.
- You can customize `placement` (`top`, `bottom`, `left`, `right`, etc.).
- Make sure the Popover is initialized with JavaScript if you need more control or multiple elements.

This approach leverages Bootstrap's built-in popover functionality for a clean, professional implementation that is easy to maintain.