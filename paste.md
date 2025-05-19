## Extracting Text and Password Input Values in JavaScript

---

**Explanation:**

When working with HTML form inputs, JavaScript allows you to access the **value** property of **input** elements to get the current user-entered data. For **text** and **password** inputs, the process is identical; it involves selecting the input element and then retrieving its `.value`.

---

### Selecting Input Elements

**Method 1: Using `getElementById()`**

- **Purpose:** To select an element with a specific `id` attribute.
- **Usage:** `document.getElementById('elementId')`

**Method 2: Using `querySelector()`**

- **Purpose:** To select elements based on CSS selectors.
- **Usage:** `document.querySelector('input[type="text"]')`

---

### Retrieving Values

- Once you have a reference to the input element, you can access its **value** property:

```javascript
const textInput = document.getElementById('textInputId');
const passwordInput = document.getElementById('passwordInputId');

const textValue = textInput.value;
const passwordValue = passwordInput.value;
```

- These variables now hold the **current text** entered in the respective input fields.

---

### Example: Complete Script with HTML

```html
<!-- HTML Part -->
<input type="text" id="textInput" placeholder="Enter text here" />
<input type="password" id="passwordInput" placeholder="Enter password" />
<button id="submitBtn">Get Values</button>

<!-- JavaScript Part -->
<script>
  document.getElementById('submitBtn').addEventListener('click', () => {
    const textVal = document.getElementById('textInput').value;
    const passVal = document.getElementById('passwordInput').value;
    console.log('Text:', textVal);
    console.log('Password:', passVal);
  });
</script>
```

**In this example:**

- When the user clicks the button, it triggers an event listener.
- The script then retrieves the **current** values from **both input fields**.
- Values are output to the console for demonstration.

---

### Summary

- Select input elements via `getElementById()` or `querySelector()`.
- Access the **`.value`** property to get the entered data.
- This approach works similarly for **text** and **password** input types.

---

**References:**

## MDN Web Docs - HTMLInputElement: https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement