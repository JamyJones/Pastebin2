To achieve this functionality in Bootstrap 5, you can use the Bootstrap `nav` component along with JavaScript to display five sections at a time dynamically. Below is a structured approach:

### **Steps to Implement**
1. Create your navigation links.
2. Organize the sections with unique IDs.
3. Use JavaScript to show only five sections at a time.

### **Example Implementation**

#### **HTML Structure**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Section Navigation</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .section { display: none; }
        .active { display: block; }
    </style>
</head>
<body>
    <div class="container mt-4">
        <ul class="nav nav-pills" id="navLinks">
            <li class="nav-item"><a class="nav-link active" href="#" data-start="0">Page 1</a></li>
            <li class="nav-item"><a class="nav-link" href="#" data-start="5">Page 2</a></li>
            <li class="nav-item"><a class="nav-link" href="#" data-start="10">Page 3</a></li>
        </ul>

        <div class="mt-4" id="sections">
            <!-- Sections -->
            <div class="section active" id="section1">Section 1</div>
            <div class="section active" id="section2">Section 2</div>
            <div class="section active" id="section3">Section 3</div>
            <div class="section active" id="section4">Section 4</div>
            <div class="section active" id="section5">Section 5</div>
            <div class="section" id="section6">Section 6</div>
            <div class="section" id="section7">Section 7</div>
            <div class="section" id="section8">Section 8</div>
            <div class="section" id="section9">Section 9</div>
            <div class="section" id="section10">Section 10</div>
        </div>
    </div>

    <script>
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', function(event) {
                event.preventDefault();
                let startIndex = parseInt(this.getAttribute('data-start'));

                document.querySelectorAll('.section').forEach((section, index) => {
                    section.classList.remove('active');
                    if (index >= startIndex && index < startIndex + 5) {
                        section.classList.add('active');
                    }
                });

                document.querySelectorAll('.nav-link').forEach(nav => nav.classList.remove('active'));
                this.classList.add('active');
            });
        });
    </script>
</body>
</html>
```

### **Explanation**
- **Navigation Links (`nav-pills`)**: Each link contains a `data-start` attribute that determines the starting section to display.
- **Section Display**: Initially, the first five sections are visible (`active` class).
- **JavaScript Event Listener**: When a navigation link is clicked, it dynamically updates the visibility of the sections based on the `data-start` value.

### **Best Practices**
- Ensure your CSS properly hides inactive sections.
- Use Bootstrap's built-in `nav` styling to enhance UX.
- Optimize JavaScript for dynamic updates without reloading the page.

This approach efficiently provides the navigation-like section display using Bootstrap 5 while keeping the logic clean and easy to manage. Let me know if you need refinements! [[0]](https://github.com/l7u7ch/absarcs/tree/7c007fc5bd21cd71bcd0c942f098143b9cb2fc62/content/How+to/2021-01-11T01_24_33+0900/index.md)



> [0] [](https://github.com/l7u7ch/absarcs/tree/7c007fc5bd21cd71bcd0c942f098143b9cb2fc62/content/How+to/2021-01-11T01_24_33+0900/index.md)