To set the value of a `<select>` HTML element using JavaScript, you can use the `value` property of the select element. Here’s a simple example:

### HTML
```html
<select id="mySelect">
    <option value="1">Option 1</option>
    <option value="2">Option 2</option>
    <option value="3">Option 3</option>
</select>
<button onclick="setSelectValue()">Set Value</button>
```

### JavaScript
```javascript
function setSelectValue() {
    var selectElement = document.getElementById("mySelect");
    selectElement.value = "2"; // Set the value to "2" (Option 2)
}
```

### Explanation
1. The `<select>` element has an `id` of `mySelect`.
2. The `setSelectValue` function retrieves the select element using `document.getElementById`.
3. It then sets the `value` property of the select element to the desired value (in this case, "2").

When you click the button, the select element will change to "Option 2".