To get the text value of a form element in JavaScript, you can use the `value` property of input elements like `<input>`, `<textarea>`, and `<select>`. Here’s how you can do it:

### 1. **For Input Fields (text, email, password, etc.)**
```javascript
const inputValue = document.getElementById("myInput").value;
console.log(inputValue); // Prints the value in the console
```
```html
<input type="text" id="myInput" />
```

### 2. **For Textarea**
```javascript
const textareaValue = document.getElementById("myTextarea").value;
console.log(textareaValue);
```
```html
<textarea id="myTextarea"></textarea>
```

### 3. **For Select Dropdown**
```javascript
const selectValue = document.getElementById("mySelect").value;
console.log(selectValue);
```
```html
<select id="mySelect">
    <option value="Option1">Option 1</option>
    <option value="Option2">Option 2</option>
</select>
```

### 4. **Using Query Selector**
If you want to use `querySelector`:
```javascript
const inputValue = document.querySelector("#myInput").value;
console.log(inputValue);
```

### Best Practices:
- Ensure the element exists before accessing its `value` property to avoid errors.
- Use event listeners (e.g., `change` or `input`) to dynamically retrieve values when the user interacts.
- Validate inputs before processing them.

Would you like to see examples with event listeners or form submissions?