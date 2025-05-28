It looks like you're using Bootstrap 5, but your code is still using the `data-toggle` attribute, which is not supported in Bootstrap 5. Instead, Bootstrap 5 uses the `data-bs-toggle` attribute for tab functionality. 

Here's how you can modify your code to make the tabs work correctly:

1. Change `data-toggle` to `data-bs-toggle`.
2. Ensure that you have included the Bootstrap 5 JavaScript library in your project, as the tab functionality relies on it.

Here’s the corrected code:

```html
<div class="container mt-5">
    <ul class="nav nav-tabs" id="authTabs" role="tablist">
        <li class="nav-item">
            <button type="button" class="nav-link active" id="login-tab" data-bs-toggle="tab" data-bs-target="#login" role="tab" aria-controls="login" aria-selected="true">Login</button>
        </li>
        <li class="nav-item">
            <button type="button" class="nav-link" id="signup-tab" data-bs-toggle="tab" data-bs-target="#signup" role="tab" aria-controls="signup" aria-selected="false">Sign Up</button>
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
                                <input id="email-entry-signup" type="text" class="form-control" placeholder="Email or Phone Number" required>
                            </div>
                            <div class="mb-3">
                                <input type="password" id="password-entry-signup" class="form-control" placeholder="Password" required>
                            </div>
                            <button type="button" id="signup-form-btn" class="btn btn-primary w-100">Sign Up</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### Additional Notes:
- Make sure to include the Bootstrap 5 CSS and JS files in your HTML. You can use the following CDN links:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
```

- Ensure that the IDs for the input fields in the signup form are unique (e.g., `id="email-entry-signup"` and `id="password-entry-signup"`), as having duplicate IDs can lead to unexpected behavior.