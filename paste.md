To get the text value of a form element (such as an input or textarea), you typically select the element using JavaScript and access its `value` property.

### 1. HTML Example:
```html
<form id="myForm">
  <input type="text" id="name" name="name" value="John Doe">
  <textarea id="message">Hello, World!</textarea>
</form>
<button id="submitBtn">Get Values</button>
```

### 2. JavaScript: Accessing the value
You can access these values in JavaScript as follows:

```javascript
// Select the input element
const nameInput = document.getElementById('name');
const messageTextarea = document.getElementById('message');

// Get the values
const nameValue = nameInput.value;
const messageValue = messageTextarea.value;

console.log('Name:', nameValue);
console.log('Message:', messageValue);
```

### 3. When to get the value
- Usually, you'd fetch the value upon a form submission or an event (like button click).

```javascript
document.getElementById('submitBtn').addEventListener('click', () => {
  const nameValue = document.getElementById('name').value;
  const messageValue = document.getElementById('message').value;
  // Use the values as needed
  alert(`Name: ${nameValue}\nMessage: ${messageValue}`);
});
```

### 4. Notes on best practices
- Always query for elements with unique IDs or specific classes.
- Avoid directly accessing properties inside event handlers without null checks.
- For multiple form elements, consider using FormData API for easier data retrieval.

---

### **Summary:**
Access the `value` property of the form element, such as:

```js
const elementValue = document.getElementById('elementId').value;
```

This applies to `<input>`, `<textarea>`, `<select>`, and other form input elements.