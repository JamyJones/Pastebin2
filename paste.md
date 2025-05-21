You want to prevent the default broken image icon from appearing when an image fails to load. A professional approach is to use the onError event handler in JavaScript or React to replace the failed image with a fallback (such as a transparent pixel or a custom placeholder).

**Example in plain HTML/JavaScript:**

```html
<img src="invalid-url.jpg" alt="Example"
     onerror="this.onerror=null; this.src='fallback.png';" />
```

**Explanation:**
- The onerror handler triggers when the image fails to load.
- Setting this.onerror = null prevents an infinite loop if the fallback also fails.
- The src is replaced with a fallback image.

**Best Practices:**
- Use a lightweight fallback (e.g., a 1x1 transparent PNG) if you want nothing visible:
  
  ```html
  <img src="invalid-url.jpg" alt="Example"
       onerror="this.onerror=null; this.src='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR4nGNgYAAAAAMAASsJTYQAAAAASUVORK5CYII=';" />
  ```

**Example in React:**

```jsx
function SafeImage({ src, alt, ...props }) {
  const fallback = 'fallback.png';
  const handleError = (e) => {
    e.target.onerror = null;
    e.target.src = fallback;
  };
  return <img src={src} alt={alt} onError={handleError} {...props} />;
}
```

**Summary:**  
Use the onError event to swap out the image source when loading fails, ensuring users never see the browser’s default broken image icon.

Let me know if you need an example for a specific framework or more details!