In JavaScript, you can work with the DOM (Document Object Model) to manipulate HTML elements, including `<img>` elements. To set properties such as the `src` attribute of an image, you can use JavaScript’s `.src` property.

### Example:

```javascript
// Select the image element
let imgElement = document.getElementById("myImage");

// Set the 'src' attribute
imgElement.src = "https://example.com/image.jpg";

// You can also modify other properties
imgElement.alt = "Example Image";
imgElement.width = 300;
imgElement.height = 200;
```

### Creating a New Image Element:

```javascript
// Create a new image element
let newImage = document.createElement("img");

// Set attributes
newImage.src = "https://example.com/new-image.jpg";
newImage.alt = "New Image";
newImage.width = 250;
newImage.height = 150;

// Append it to the document
document.body.appendChild(newImage);
```

### Best Practices:
1. **Ensure the image URL is valid** to avoid broken links.
2. **Use `alt` attributes** for accessibility and SEO.
3. **Optimize image sizes** to enhance page load speed.
4. **Lazy loading (`loading="lazy"`)** can improve performance.
5. **Event Listeners** can be used to handle image loading errors:

```javascript
imgElement.onerror = function() {
    console.log("Image failed to load. Please check the URL.");
};
```

These techniques help manage images dynamically within a web application efficiently! Let me know if you need further clarification.