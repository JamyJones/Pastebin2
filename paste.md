In Bootstrap 5, the `<input type="file">` element is styled using Bootstrap's custom file input classes to create a consistent and visually appealing UI for file uploads, including images.

### How it works:

- The native file input element (`<input type="file">`) is styled to look better across browsers.
- Bootstrap 5 provides utility classes like `.form-control` and specific custom classes (`.form-control-file`) to enhance appearance.
- To create a more user-friendly experience, Bootstrap 5 recommends using custom file input markup with the `.form-file` class, although Bootstrap 5 has simplified this compared to earlier versions.

### Basic example:

```html
<div class="mb-3">
  <label for="formFile" class="form-label">Upload Image</label>
  <input class="form-control" type="file" id="formFile" accept="image/*">
</div>
```
- `accept="image/*"` restricts user file selection to image files.
  
### Enhancing with custom labels:
Bootstrap 5 allows for a custom label that updates with the selected filename.

```html
<div class="mb-3">
  <label for="formFile" class="form-label">Upload Image</label>
  <input class="form-control" type="file" id="formFile" accept="image/*">
</div>
```

### Making the filename display dynamic:

Bootstrap 5 provides `.form-label`, but to show the filename, you'll use JavaScript.

```html
<div class="mb-3">
  <label for="formFile" class="form-label">Upload Image</label>
  <input class="form-control" type="file" id="formFile" accept="image/*">
  <div class="mt-2" id="fileName"></div>
</div>

<script>
  document.getElementById('formFile').addEventListener('change', function() {
    const fileNameDisplay = document.getElementById('fileName');
    if (this.files.length > 0) {
        fileNameDisplay.textContent = `Selected file: ${this.files[0].name}`;
    } else {
        fileNameDisplay.textContent = '';
    }
  });
</script>
```

### Additional best practices:
- **Multiple Files:** Add `multiple` attribute if multiple images can be uploaded:

```html
<input class="form-control" type="file" id="formFileMultiple" accept="image/*" multiple>
```

- **Server-side handling:** On the backend, ensure you process uploaded images securely, validate file types, sizes, and handle storage appropriately.

### Summary:

- Bootstrap 5's styling makes file inputs more consistent.
- Use `accept` attribute for image files.
- JavaScript enhances UX by showing selected filenames.
- Always validate and sanitize files server-side.

Would you like a complete example including image preview or server integration?