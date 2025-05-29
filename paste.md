Here’s a beautified version of your message using HTML and Bootstrap 5:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <title>Welcome Message</title>
</head>
<body>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header text-center">
                <h2>Welcome to Our Application!</h2>
            </div>
            <div class="card-body">
                <p class="lead">Thank you for signing up! To complete your registration, please check your email inbox for a confirmation email.</p>
                <p>Inside the email, you will find a confirmation link. Click on this link to verify your account.</p>
                <p>Once your account is verified, return to the login page and log in using your email and password.</p>
                <p class="text-warning">If you do not see the email in your inbox, please check your spam or junk folder.</p>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

### Explanation:
- The message is wrapped in a Bootstrap card for a clean and modern look.
- The header is centered and styled with a larger font size.
- The body contains the message with appropriate spacing and emphasis.
- A warning style is applied to the last paragraph to draw attention to the note about checking the spam folder.