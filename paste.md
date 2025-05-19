## summary  
**Retrieving text and password input values in JavaScript**

---  

### Explanation:  

**1. Selecting the Input Elements**  
Use `document.getElementById()` or `document.querySelector()` to reference your `<input>` elements.  
```js
const textInput = document.getElementById('textInputId'); // For text input
const passwordInput = document.getElementById('passwordInputId'); // For password input
```
*(Ensure your input elements have corresponding `id` attributes in HTML)*

**2. Accessing the Value Property**  
Each input element has a `.value` property that stores user input. To get the current value:  
```js
const textValue = textInput.value; // Retrieves current value of text input
const passwordValue = passwordInput.value; // Retrieves current value of password input
```

**3. Practical Example**  
```html
<input type="text" id="textInputId" placeholder="Enter text here" />
<input type="password" id="passwordInputId" placeholder="Enter password" />
<button onclick="getInputValues()">Get Values</button>
<script>
  function getInputValues() {
    const textInput = document.getElementById('textInputId');
    const passwordInput = document.getElementById('passwordInputId');

    const textValue = textInput.value;
    const passwordValue = passwordInput.value;

    alert(`Text: ${textValue}\nPassword: ${passwordValue}`);
  }
</script>
```
*(Clicking the button triggers the `getInputValues()` function, which retrieves and displays the current input values.)*

---

### References  
## https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input##