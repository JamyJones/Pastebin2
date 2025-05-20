When creating a chat app where users can upload profile pictures, following industry best practices for image sizes ensures good performance, quality, and consistency across devices. 

### Recommended Profile Picture Sizes

1. **Optimal upload size:**  
   - **Range:** 200x200 pixels to 400x400 pixels  
   - **Why:** Small enough to upload quickly, large enough to look good on high-resolution displays and when zoomed in.

2. **Maximum upload resolution:**  
   - Typically, you can set a maximum file size (e.g., **1MB or less**) and dimensions (e.g., **800x800 pixels**) to prevent excessively large images.

3. **Display sizes in the app:**  
   - **Profile thumbnail:** 50x50 or 100x100 pixels for avatar display in chat lists.  
   - **Detailed profile view:** 200x200 or 300x300 pixels for profile pages.

### Best Practice Guidelines

- **Resize images server-side** to a consistent dimension (e.g., 400x400) to ensure uniformity.
- Use **responsive images** or different sizes for various contexts (thumbnails vs. full view).
- Convert images to efficient formats like **JPEG or WebP** for a good balance of quality and compression.
- Consider implementing **client-side resizing** before upload to improve upload speed and reduce server load.

### Example

Suppose you are using **JavaScript and Canvas API** to resize images client-side before uploading:

```javascript
function resizeImage(file, maxWidth, maxHeight, callback) {
  const reader = new FileReader();

  reader.onload = function(event) {
    const img = new Image();
    img.onload = function() {
      let width = img.width;
      let height = img.height;

      // Calculate resize ratio
      const ratio = Math.min(maxWidth / width, maxHeight / height);
      width *= ratio;
      height *= ratio;

      // Create canvas
      const canvas = document.createElement('canvas');
      canvas.width = width;
      canvas.height = height;

      const ctx = canvas.getContext('2d');
      ctx.drawImage(img, 0, 0, width, height);

      // Convert to Data URL (you can also get Blob for upload)
      canvas.toBlob((blob) => {
        callback(blob);
      }, 'image/jpeg', 0.8);
    };
    img.src = event.target.result;
  };
  reader.readAsDataURL(file);
}
```

### Summary

- **Recommended size for profile pictures:** 200x200 to 400x400 pixels.
- **Maximum upload size:** Keep under 1MB.
- Resize images server-side for consistency.
- Provide different display sizes (thumbnails, profile view).

This approach balances image quality, performance, and user experience in a professional chat application.