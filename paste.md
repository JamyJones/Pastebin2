To create a single-page application with Bootstrap 5 that displays five sections and allows navigation between them, you can use Bootstrap's built-in components like the Navbar and Scrollspy. Below is a simple example of how to set this up.

### HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Single Page Navigation</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        section {
            height: 100vh; /* Full viewport height for each section */
            padding: 20px;
        }
    </style>
</head>
<body data-bs-spy="scroll" data-bs-target="#navbar" data-bs-offset="70" tabindex="0">

    <nav id="navbar" class="navbar navbar-expand-lg navbar-light bg-light fixed-top">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">My App</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <a class="nav-link" href="#section1">Section 1</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#section2">Section 2</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#section3">Section 3</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#section4">Section 4</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#section5">Section 5</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <div class="container mt-5 pt-5">
        <section id="section1" class="bg-primary text-white">
            <h1>Section 1</h1>
            <p>This is the content of Section 1.</p>
        </section>
        <section id="section2" class="bg-secondary text-white">
            <h1>Section 2</h1>
            <p>This is the content of Section 2.</p>
        </section>
        <section id="section3" class="bg-success text-white">
            <h1>Section 3</h1>
            <p>This is the content of Section 3.</p>
        </section>
        <section id="section4" class="bg-danger text-white">
            <h1>Section 4</h1>
            <p>This is the content of Section 4.</p>
        </section>
        <section id="section5" class="bg-warning text-dark">
            <h1>Section 5</h1>
            <p>This is the content of Section 5.</p>
        </section>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.6/dist/umd/popper.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.min.js"></script>
</body>
</html>
```

### Explanation

1. **Navbar**: The navigation bar is created using Bootstrap's Navbar component. Each link in the navbar corresponds to a section on the page.

2. **Sections**: Each section has a unique ID that matches the href attribute of the corresponding navbar link. This allows the page to scroll to the correct section when a link is clicked.

3. **Scrollspy**: The `data-bs-spy="scroll"` attribute on the body enables Bootstrap's Scrollspy feature, which automatically updates the active class on the navbar links as you scroll through the sections.

4. **Styling**: Each section is given a height of 100vh (full viewport height) and some padding for better visibility.

5. **JavaScript**: Bootstrap's JavaScript and Popper.js are included for the navbar toggler functionality.

You can customize the content and styles of each section as needed. This setup provides a smooth navigation experience within a single-page application.