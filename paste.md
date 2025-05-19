## Getting Text Value from Text and Password Input Elements in JavaScript <br>

---
### Retrieving Values from Input Fields <br>

When working with HTML forms, you often need to retrieve values entered by users into input elements, such as text and password fields. JavaScript provides a simple way to get these values using the `value` property of the `input` element.

---
### Accessing Input Fields Using `document.getElementById()` <br>

The most common method to access an input field is by using the `document.getElementById()` function. This requires assigning an `id` to each input field in your HTML.

#### Example:

```html
<input type="text" id="username" placeholder="Enter your username">
<input type="password" id="password" placeholder="Enter your password">
<button onclick="getValues()">Submit</button>

<script>
  function getValues() {
    // Access input elements by ID
    let username = document.getElementById("username").value;
    let password = document.getElementById("password").value;

    // Display values (avoid showing passwords in a real-world application)
    console.log("Username:", username);
    console.log("Password:", password);
  }
</script>
```

---
### Accessing Input Fields Using `querySelector()` <br>

If you prefer a more flexible approach, you can use `document.querySelector()` which allows you to access elements using CSS selectors.

#### Example:

```html
<input type="text" class="input-field username" placeholder="Enter your username">
<input type="password" class="input-field password" placeholder="Enter your password">
<button onclick="getValues()">Submit</button>

<script>
  function getValues() {
    // Access input elements using class selectors
    let username = document.querySelector(".username").value;
    let password = document.querySelector(".password").value;

    console.log("Username:", username);
    console.log("Password:", password);
  }
</script>
```

---
### Handling Input in Forms Using `event.target` <br>

Instead of using `getElementById()`, we can use the `event` object in an event listener to capture input field values dynamically.

#### Example:

```html
<form onsubmit="getValues(event)">
  <input type="text" name="username" placeholder="Enter your username">
  <input type="password" name="password" placeholder="Enter your password">
  <button type="submit">Submit</button>
</form>

<script>
  function getValues(event) {
    event.preventDefault(); // Prevent form submission

    let form = event.target;
    let username = form.username.value;
    let password = form.password.value;

    console.log("Username:", username);
    console.log("Password:", password);
  }
</script>
```

---
### Security Considerations for Password Handling <br>

When working with passwords:
- **Never log passwords in the console** in a real-world scenario.
- Use **secure hashing** mechanisms before sending passwords to a server.
- Avoid storing plaintext passwords in local storage or cookies.

---
### Conclusion <br>

Retrieving text and password values in JavaScript is straightforward using:
- `document.getElementById()`
- `document.querySelector()`
- `event.target` in event handlers

Each method depends on the structure of your HTML, and it's important to ensure security best practices when dealing with password fields.

---
### References <br>

## https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById ##
## https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector ##
## https://developer.mozilla.org/en-US/docs/Web/API/Event ##
