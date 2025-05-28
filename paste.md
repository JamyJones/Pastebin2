You can create a Bootstrap tabbed interface for user authentication with separate tabs for login and signup. Below is a complete HTML snippet that includes the necessary Bootstrap structure and your provided code for both the login and signup forms.

Make sure to include Bootstrap CSS and JS in your project for the tabs to function properly. Here’s how you can set it up:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Authentication</title>
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-5">
    <ul class="nav nav-tabs" id="authTabs" role="tablist">
        <li class="nav-item">
            <a class="nav-link active" id="login-tab" data-toggle="tab" href="#login" role="tab" aria-controls="login" aria-selected="true">Login</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" id="signup-tab" data-toggle="tab" href="#signup" role="tab" aria-controls="signup" aria-selected="false">Sign Up</a>
        </li>
    </ul>
    <div class="tab-content" id="authTabsContent">
        <div class="tab-pane fade show active" id="login" role="tabpanel" aria-labelledby="login-tab">
            <div class="container d-flex justify-content-center align-items-center vh-100">
                <div class="card p-4" style="width: 350px;">
                    <h2 class="text-center mb-3">Log in</h2>
                    <form>
                        <div class="mb-3">
                            <input type="email" id="email-entry" class="form-control" placeholder="Email or phone number" required>
                        </div>
                        <div class="mb-3">
                            <input type="password" id="password-entry" class="form-control" placeholder="Password" required>
                        </div>
                        <button type="button" id="login-form-submit" class="btn btn-primary w-100">Log In</button>
                        <hr>
                        <div class="text-center">
                            <a href="signup" class="btn btn-success">Create New Account</a>
                        </div>
                    </form>
                </div>
            </div>
        </div>
        <div class="tab-pane fade" id="signup" role="tabpanel" aria-labelledby="signup-tab">
            <div class="container my-5">
                <div class="row justify-content-center">
                    <div class="col-md-6">
                        <form>
                            <h2 class="mb-4 text-center">Sign Up</h2>
                            <div class="mb-3">
                                <input id="email-entry" type="text" class="form-control" placeholder="Email or Phone Number" required>
                            </div>
                            <div class="mb-3">
                                <input type="password" id="password-entry" class="form-control" placeholder="Password" required>
                            </div>
                            <button type="button" id="signup-form-btn" class="btn btn-primary w-100">Sign Up</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.2/dist/umd/popper.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>
```

### Explanation:
- The code creates a tabbed interface using Bootstrap's nav-tabs component.
- The `tab-content` div contains two `tab-pane` divs, one for the login form and one for the signup form.
- The login form is set as the active tab by default.
- Bootstrap's JavaScript and jQuery are included at the bottom of the document to enable tab functionality. 

Make sure to test the code in a browser to see the tabs in action!