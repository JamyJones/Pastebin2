In Bootstrap, you can use the built-in Popper.js integration to display a popper when hovering over a button. Here’s how you can do it using Bootstrap’s tooltip component:

### Steps:
1. Ensure Bootstrap and Popper.js are included in your project.
2. Add the `data-bs-toggle="tooltip"` attribute to the button element.
3. Initialize the tooltip using JavaScript.

### Example:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bootstrap Popper</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

    <div class="container mt-5">
        <button type="button" class="btn btn-primary" data-bs-toggle="tooltip" data-bs-placement="top" title="Hovered Popper">
            Hover Me
        </button>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Enable tooltips everywhere
        document.addEventListener("DOMContentLoaded", function () {
            var tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'));
            var tooltipList = tooltipTriggerList.map(function (tooltipTriggerEl) {
                return new bootstrap.Tooltip(tooltipTriggerEl);
            });
        });
    </script>

</body>
</html>
```
### Explanation:
- The `data-bs-toggle="tooltip"` attribute enables the tooltip functionality.
- The `title` attribute sets the popper content.
- The JavaScript snippet initializes tooltips on elements with `data-bs-toggle="tooltip"`.

Let me know if you need customization or additional functionality! [[0]](https://github.com/sadeghisalar/List-of-cities-in-the-Islamic-Republic-Of-Iran/tree/df469d2f2a3390e0d0638d0dea65778ff3c79c77/README.md) [[1]](https://github.com/ferhado/smoothscroll/tree/4ff228333a824dff212c1ec886272d2785e3df0e/README.md) [[2]](https://github.com/musicman3/eMarket/tree/7444ac2c466ba64acc1dcaf0923a2f50a2694ba8/src/eMarket/view/default/catalog/constructor.php) [[3]](https://github.com/acen20/flexy-dashboards/tree/a6f926510abb9560638b57a5dafb12d39b72d7dc/package/dist/js/custom.js)



> [0] [](https://github.com/sadeghisalar/List-of-cities-in-the-Islamic-Republic-Of-Iran/tree/df469d2f2a3390e0d0638d0dea65778ff3c79c77/README.md)
>
> [1] [](https://github.com/ferhado/smoothscroll/tree/4ff228333a824dff212c1ec886272d2785e3df0e/README.md)
>
> [2] [](https://github.com/musicman3/eMarket/tree/7444ac2c466ba64acc1dcaf0923a2f50a2694ba8/src/eMarket/view/default/catalog/constructor.php)
>
> [3] [](https://github.com/acen20/flexy-dashboards/tree/a6f926510abb9560638b57a5dafb12d39b72d7dc/package/dist/js/custom.js)