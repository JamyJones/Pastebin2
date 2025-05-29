To set the value of a `<select>` HTML element programmatically, you can do so using JavaScript in a few ways. The most common approach is to set the `value` property of the `<select>` element to match one of its `<option>` elements' `value` attribute.

### Example: Setting the value using JavaScript

#### HTML:
```html
<select id="mySelect">
  <option value="1">Option 1</option>
  <option value="2">Option 2</option>
  <option value="3">Option 3</option>
</select>
```

#### JavaScript:
```js
// Get the select element by ID
const selectElement = document.getElementById('mySelect');

// Set the value to '2'
selectElement.value = '2';
```

This will programmatically select the `<option>` with `value="2"`.

---

### Important points to consider:
- The `value` you assign must match the `value` attribute of one of the `<option>` elements.
- If there's no matching option, the select will not update its checked option.
- To set the selected option by its display text (not value), you need to iterate options:

```js
// Set selected option by display text
const desiredText = 'Option 3';

for (const option of selectElement.options) {
  if (option.text === desiredText) {
    selectElement.value = option.value; // or directly set option.selected = true
    break;
  }
}
```

---

### Alternative: Setting `selected` attribute directly
Alternatively, you can directly set the `selected` attribute on an `<option>`:

```js
// Select the option with specific value
for (const option of selectElement.options) {
  if (option.value === '2') {
    option.selected = true;
  } else {
    option.selected = false; // Deselect others
  }
}
```

### Summary:
- Use `selectElement.value = 'desired_value'` when you know the value.
- Ensure the value exists in options.
- You can also interact with options directly for more complex selections.

Let me know if you'd like a full example integrating event handling or dynamic options!