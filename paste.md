## Getting Text Value from Text and Password Input Elements in HTML <br>
---<br>

### Explanation:<br>

**1. Accessing Input Elements in JavaScript**<br>
To retrieve the value entered in a text or password input field, you need to first select the element in JavaScript. You can use the `document.getElementById()` or `document.querySelector()` method for this.<br>

**2. Retrieving the Text Value**<br>
Once you have selected the element, you can access the `value` property of the input element to obtain the text entered by the user.<br>

**3. Applying This to Text and Password Inputs**<br>
The process is the same for both `<input type="text">` and `<input type="password">`. The only difference is that the password input obscures the characters visually but still stores them as a value.<br>

---

### Example:<br>
Here is a practical example demonstrating how to retrieve the values from both a text and password input:<br>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Retrieve Input Values</title>
</head>
<body>
    <label for="username">Username:</label>
    <input type="text" id="username"><br><br>

    <label for="password">Password:</label>
    <input type="password" id="password"><br><br>

    <button onclick="getValues()">Submit</button>

    <script>
        function getValues() {
            // Selecting the input elements
            let username = document.getElementById("username").value;
            let password = document.getElementById("password").value;
            
            // Displaying the values
            alert("Username: " + username + "\nPassword: " + password);
        }
    </script>
</body>
</html>
```

**Breakdown of the Code:**<br>
- `document.getElementById("username").value;` → Retrieves the entered text from the username input field.<br>
- `document.getElementById("password").value;` → Retrieves the password entered in the password input field.<br>
- `alert("Username: " + username + "\nPassword: " + password);` → Displays the retrieved values in an alert box.<br>

---

### Notes:<br>
- The `value` property of an input element is used to fetch the entered content.<br>
- The `alert()` function is used here for demonstration but in a real-world scenario, you might store values in a database or perform validation.<br>
- For security reasons, avoid logging passwords directly in a console or storing them in plain text.<br>

---

#### Hope this helps! 🚀 Let me know if you need further clarification.<br> [[0]](https://github.com/buribalazs/smooth-drag-order/tree/7b40d21d076c3e31765f61481f537beaf4c5ec9f/README.md)



> [0] [](https://github.com/buribalazs/smooth-drag-order/tree/7b40d21d076c3e31765f61481f537beaf4c5ec9f/README.md)