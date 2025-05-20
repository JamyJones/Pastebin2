In front-end development, retrieving the text value of a form element is a common task that can be achieved using JavaScript. Here’s a professional approach to handling this:

### Using JavaScript to Get the Text Value

#### 1. **Using `value` Property for Input Fields**
For text inputs, you can use the `.value` property.

```html
<form id="myForm">
    <input type="text" id="textInput" placeholder="Enter text here">
    <button type="button" onclick="getTextValue()">Submit</button>
</form>

<script>
function getTextValue() {
    const textValue = document.getElementById("textInput").value;
    console.log("Entered text:", textValue);
}
</script>
```

#### 2. **Using `textContent` or `innerText` for Non-Input Elements**
If you’re working with elements like `<span>`, `<div>`, or `<p>`, use `.textContent` or `.innerText`.

```html
<p id="displayText">Hello, World!</p>
<button type="button" onclick="getParagraphText()">Get Text</button>

<script>
function getParagraphText() {
    const textValue = document.getElementById("displayText").textContent;
    console.log("Paragraph text:", textValue);
}
</script>
```

### Best Practices:
- **Use `value` for input elements** such as `<input>` and `<textarea>`.
- **Use `textContent` for standard text elements** like `<p>` and `<span>`, avoiding `innerText` unless you need styling considerations.
- **Validate input values** to prevent security risks like XSS (Cross-Site Scripting).
- **Use event listeners** instead of inline `onclick` attributes for better maintainability.

Would you like examples on retrieving values in different frameworks like React or Vue?