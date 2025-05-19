## Retrieving Text and Password Input Values in JavaScript

---

### Explanation:

In HTML, `<input>` elements are commonly used to receive user input, such as text and passwords. To access their values using JavaScript, you need to select the input element and then read its `value` property.

---

### How to get the value of a text input element:

```javascript
// Step 1: Select the input element by its ID
const textInput = document.getElementById('textInputId');

// Step 2: Access the 'value' property
const textValue = textInput.value;

console.log(textValue);
```

**Breakdown:**
- **`document.getElementById('textInputId')`**: This fetches the HTML element with the specific ID.
- **`.value`**: Retrieves the current value inside the input box.

---

### How to get the value of a password input element:

```javascript
// Step 1: Select the password input by its ID
const passwordInput = document.getElementById('passwordInputId');

// Step 2: Access its value
const passwordValue = passwordInput.value;

console.log(passwordValue);
```

**Note:** Both input types (`text` and `password`) in HTML are similar in behavior regarding retrieving their values; the main difference lies in how they display user input on the page.

---

### Example: Complete HTML & JavaScript

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<title>Input Values Example</title>
</head>
<body>

<!-- Text Input -->
<input type="text" id="textInputId" placeholder="Enter text here" />

<!-- Password Input -->
<input type="password" id="passwordInputId" placeholder="Enter password" />

<!-- Button to trigger value fetch -->
<button onclick="fetchInputValues()">Get Values</button>

<script>
function fetchInputValues() {
  const textValue = document.getElementById('textInputId').value;
  const passwordValue = document.getElementById('passwordInputId').value;

  alert('Text Input: ' + textValue + '\nPassword Input: ' + passwordValue);
}
</script>

</body>
</html>
```

---

### References:
##MDN Web Docs - `<input>` HTML Element##
##https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input##