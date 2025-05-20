Certainly! Below is a professional CSS animation class that smoothly animates a button when hovered over. This class can be applied to your Bootstrap-based form submission button.

```css
/* Define the animation */
@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
}

/* Apply animation to the button */
.btn-animate {
  transition: all 0.3s ease-in-out;
}

.btn-animate:hover {
  animation: pulse 0.6s infinite;
}
```

### How to Use:
Add the `btn-animate` class alongside your Bootstrap button class (e.g., `btn-primary` or `btn-success`) in your HTML:

```html
<button type="submit" class="btn btn-primary btn-animate">Submit</button>
```

### Explanation:
- The `@keyframes` rule defines a smooth "pulse" animation that enlarges the button slightly when hovered.
- The `.btn-animate` class ensures smooth transition effects for the hover state.
- The animation runs infinitely while the button is hovered, creating an eye-catching effect.

Let me know if you need modifications!