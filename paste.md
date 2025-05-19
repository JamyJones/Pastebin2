## How to retrieve text and password input values in JavaScript

--- 
### Explanation:

**This guide explains the methods for accessing the values of `<input>` elements of types `text` and `password` in HTML using JavaScript.**

---

### Basic Approach:

When working with HTML forms, each `<input>` element can be accessed via JavaScript using its `id`, `name`, or other DOM features, and then reading its `value` property.

---

### Step-by-step Process:

#### 1. **Assign IDs to your input elements**

```html
<input type="text" id="myTextInput" />
<input type="password" id="myPasswordInput" />
```

- **Why?** Using IDs makes it straightforward to target specific elements via JavaScript with `document.getElementById`.

---

#### 2. **Retrieve the values with JavaScript**

```javascript
// Get references to the input elements
const textInput = document.getElementById('myTextInput');
const passwordInput = document.getElementById('myPasswordInput');

// Access the 'value' property
const textValue = textInput.value;
const passwordValue = passwordInput.value;
```

- **What each line does:**

| Line | Function | Explanation |
|--------|---------|--------------|
| `document.getElementById('myTextInput')` | Finds the HTML element with the specified ID | Returns the DOM element, which can be used to access properties like `value` |
| `.value` | Property of `<input>` elements | Contains the current value entered by the user |

---

### When to retrieve values

Usually, values are retrieved in response to an event, such as a button click:

```html
<button onclick="getValues()">Get Input Values</button>
```

```javascript
function getValues() {
  const text = document.getElementById('myTextInput').value;
  const password = document.getElementById('myPasswordInput').value;
  console.log('Text:', text);
  console.log('Password:', password);
}
```

- The function `getValues()` will execute when the button is clicked, grabbing and printing current input values.

---

### Example: Full HTML + JavaScript snippet

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Input Values</title>
</head>
<body>

<input type="text" id="myTextInput" placeholder="Enter text here" />
<input type="password" id="myPasswordInput" placeholder="Enter password" />

<button onclick="getValues()">Get Input Values</button>

<script>
function getValues() {
    const textValue = document.getElementById('myTextInput').value;
    const passwordValue = document.getElementById('myPasswordInput').value;
    alert('Text Input: ' + textValue + '\nPassword Input: ' + passwordValue);
}
</script>

</body>
</html>
```

---
### References:
## MDN Web Docs on `<input>` element: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input