You’d like an animation class for an image element while it’s loading, using Bootstrap. Here’s a professional approach using CSS for a simple shimmer effect, which is commonly used as a loading placeholder:

```css
/* Add this to your stylesheet */
.img-loading {
  position: relative;
  overflow: hidden;
  background: #e0e0e0;
}

.img-loading::after {
  content: '';
  display: block;
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
  animation: shimmer 1.5s infinite;
}

@keyframes shimmer {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}
```

**Usage Example in HTML:**
```html
<img src="your-image.jpg" class="img-fluid img-loading" alt="Loading..." />
```

**Best Practices:**
- Remove the .img-loading class once the image has loaded (using JavaScript’s `onload` event).
- Ensure accessibility by keeping the `alt` attribute meaningful.

**JavaScript Example to Remove the Class on Load:**
```javascript
const img = document.querySelector('img.img-loading');
img.onload = function() {
  img.classList.remove('img-loading');
};
```

Let me know if you need a React/Vue/Angular example or further customization.