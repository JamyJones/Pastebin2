To remove a file that has been added to an `<input type="file">` element using JavaScript, you can simply reset its value. Here's how you can do it:

### Using JavaScript
```javascript
document.getElementById("fileInput").value = "";
```
This method works well for clearing a selected file from an input field.

### Full Example
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Remove File from Input</title>
</head>
<body>

    <input type="file" id="fileInput">
    <button onclick="clearFile()">Remove File</button>

    <script>
        function clearFile() {
            document.getElementById("fileInput").value = "";
        }
    </script>

</body>
</html>
```
### Important Notes:
1. The `.value` property of a file input can be set to an empty string to clear the selected file.
2. This approach may not work in some older browsers due to security restrictions, so an alternative is to **replace the element dynamically**:

```javascript
function resetFileInput() {
    const fileInput = document.getElementById("fileInput");
    const newInput = document.createElement("input");
    newInput.type = "file";
    newInput.id = "fileInput";
    fileInput.parentNode.replaceChild(newInput, fileInput);
}
```
This method ensures a fresh `<input>` element is used, removing any restrictions related to `.value` manipulations.

Would you like further improvements or explanations? [[0]](https://github.com/buribalazs/smooth-drag-order/tree/7b40d21d076c3e31765f61481f537beaf4c5ec9f/README.md) [[1]](https://github.com/ValonJashari/FE21-PHP-DAY04-ValiJashari/tree/03185eea8c9935612841fa4ccb1b2960dbd3e981/delete.php)



> [0] [](https://github.com/buribalazs/smooth-drag-order/tree/7b40d21d076c3e31765f61481f537beaf4c5ec9f/README.md)
>
> [1] [](https://github.com/ValonJashari/FE21-PHP-DAY04-ValiJashari/tree/03185eea8c9935612841fa4ccb1b2960dbd3e981/delete.php)