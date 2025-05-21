Certainly! To add a custom animation class for an image that appears while the image is loading, you can create a CSS class with desired animation effects and add it dynamically using JavaScript when the image starts loading. Once the image has loaded, you can remove the animation class.

Here's a professional approach:

### 1. Define the CSS animation class

Let's create a simple skeleton loading animation as an example:

```css
/* Define the keyframes for loading animation */
@keyframes pulse {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}

.loading-animation {
  display: inline-block;
  width: 100%;
  height: 100%;
  background-color: #e0e0e0; /* fallback background */
  animation: pulse 1.5s infinite ease-in-out;
}
```

### 2. JavaScript to add/remove the class

Here's a snippet that applies the animation class while the image is loading and removes it after load:

```js
// Select your image element
const img = document.querySelector('img');

function addLoadingAnimation(imgElement) {
  // Add the animation class
  imgElement.classList.add('loading-animation');

  // Optional: set a background placeholder
  // imgElement.style.backgroundColor = '#e0e0e0';

  // Attach load event to remove animation once loaded
  imgElement.addEventListener('load', () => {
    imgElement.classList.remove('loading-animation');
    // Remove event listener after firing
    imgElement.removeEventListener('load', arguments.callee);
  });

  // For browsers that might cache images, trigger load event
  if (imgElement.complete) {
    // Image already loaded
    imgElement.classList.remove('loading-animation');
  }
}

// Usage
addLoadingAnimation(img);
```

### 3. Usage in your HTML

```html
<img src="your-image.jpg" alt="Loading example" />

<script>
  const img = document.querySelector('img');
  addLoadingAnimation(img);
</script>
```

---

### Best practices:
- **Ensure the animation is consistent with your UI/UX**
- **Set a fallback or placeholder background during loading**
- **Handle cached images with the `complete` property**
- **Remove event listeners after they fire to prevent memory leaks**

This setup improves user experience by visually indicating loading status, aligning with professional development standards.