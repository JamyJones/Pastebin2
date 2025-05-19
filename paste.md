## Setting Actions for the Submit Button in a Bootstrap Login Form  
---  
### Explanation  
#### Handling Form Submission  
To set actions for the **submit** button in a Bootstrap login form, you need to define how the form should behave when submitted. The common methods include:
- Using **HTML forms** with an `action` attribute to direct data submission.
- Handling submissions via **JavaScript** for custom validation or AJAX requests.
- Using **backend processing** (e.g., PHP, Node.js) to verify credentials.  
---  
#### Using HTML Form Action Attribute  
In pure **HTML**, the form submission is typically handled by setting the `action` attribute within the `<form>` tag, which directs the request to a server-side script.

```html
<form action="login.php" method="POST">
    <input type="text" name="username" class="form-control" placeholder="Username">
    <input type="password" name="password" class="form-control" placeholder="Password">
    <button type="submit" class="btn btn-primary">Login</button>
</form>
```
- The `action="login.php"` ensures that data is sent to `login.php` for processing.
- The `method="POST"` ensures sensitive data like passwords is transmitted securely.  
---  
#### Handling Submission with JavaScript  
If you want to **prevent default behavior** and handle login validation with **JavaScript**, you can use the `onsubmit` event listener.

```html
<form id="loginForm">
    <input type="text" id="username" class="form-control" placeholder="Username">
    <input type="password" id="password" class="form-control" placeholder="Password">
    <button type="submit" class="btn btn-primary">Login</button>
</form>

<script>
document.getElementById("loginForm").addEventListener("submit", function(event){
    event.preventDefault(); // Prevents form submission
    let username = document.getElementById("username").value;
    let password = document.getElementById("password").value;
    
    if(username && password) {
        alert("Login successful!");
        // Send credentials to backend via AJAX if needed
    } else {
        alert("Please enter both fields.");
    }
});
</script>
```
- `event.preventDefault();` stops the default form submission.
- Retrieves `username` and `password` values for validation.
- Alerts the user if credentials are missing or process data.  
---  
#### Backend Processing Example (PHP)  
To **process credentials**, a backend script can verify user login details.

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST["username"];
    $password = $_POST["password"];

    if ($username == "admin" && $password == "12345") {
        echo "Login successful!";
    } else {
        echo "Invalid credentials.";
    }
}
?>
```
- **`$_POST`** retrieves submitted data.
- Credentials are checked against a predefined set.
- Responds with success or error messages.  
---  
### Example  
A Bootstrap login form integrating JavaScript validation and backend processing:

```html
<form id="loginForm" action="login.php" method="POST">
    <input type="text" name="username" id="username" class="form-control" placeholder="Username">
    <input type="password" name="password" id="password" class="form-control" placeholder="Password">
    <button type="submit" class="btn btn-primary">Login</button>
</form>

<script>
document.getElementById("loginForm").addEventListener("submit", function(event){
    if (!document.getElementById("username").value || !document.getElementById("password").value) {
        event.preventDefault(); 
        alert("Please fill all fields!");
    }
});
</script>
```
This setup ensures:
- **Basic Bootstrap styling**
- **Client-side validation with JavaScript**
- **Form submission handled by backend (PHP or Node.js)**  

Would you like further customization on handling authentication or UI enhancements? 🚀 [[0]](https://github.com/zaidanriski/web-rpl2share/tree/1ae3d0a0a6836dbd7e7475377b56530a2fcb14b0/index.php) [[1]](https://github.com/geraldon1997/bossearn/tree/dcf788556b568c6f08d8fc4317434febfc9f9a78/login.php) [[2]](https://github.com/absmugz/codeigniter_jquizme/tree/94a50fc73e4c00224938fe7b191a4650939c5b67/application/views/home_view.php) [[3]](https://github.com/Thienanh-682/Module2-session1/tree/25aec2cb4550e77215ee4a8e449b644a1c0e08e1/chucnangdangnhap.php) [[4]](https://github.com/Orel-Id/BoardGame/tree/19756acc724fc0f16d4f54456922953eb27d2701/Views/connexion.php) [[5]](https://github.com/FirebirdRobotics/Scouting_App/tree/bc1c14d240972d79e53c800d7bd9b106841b4b2d/Scouting+App/WebContent/index.php)



> [0] [](https://github.com/zaidanriski/web-rpl2share/tree/1ae3d0a0a6836dbd7e7475377b56530a2fcb14b0/index.php)
>
> [1] [](https://github.com/geraldon1997/bossearn/tree/dcf788556b568c6f08d8fc4317434febfc9f9a78/login.php)
>
> [2] [](https://github.com/absmugz/codeigniter_jquizme/tree/94a50fc73e4c00224938fe7b191a4650939c5b67/application/views/home_view.php)
>
> [3] [](https://github.com/Thienanh-682/Module2-session1/tree/25aec2cb4550e77215ee4a8e449b644a1c0e08e1/chucnangdangnhap.php)
>
> [4] [](https://github.com/Orel-Id/BoardGame/tree/19756acc724fc0f16d4f54456922953eb27d2701/Views/connexion.php)
>
> [5] [](https://github.com/FirebirdRobotics/Scouting_App/tree/bc1c14d240972d79e53c800d7bd9b106841b4b2d/Scouting+App/WebContent/index.php)