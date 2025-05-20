Certainly! Since you're using Bootstrap, you can enhance the submit button's interaction by adding a simple CSS animation. Below is a CSS animation that creates a subtle scaling effect when the button is clicked:

```css
@keyframes buttonPress {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(0.95);
  }
  100% {
    transform: scale(1);
  }
}

.submit-btn {
  animation: buttonPress 0.3s ease-in-out;
}
```

### How to Use It:
1. Add the `submit-btn` class to your button element.
2. Use Bootstrap's built-in classes for styling and responsiveness.

Here's an example of how your button might look:

```html
<button type="submit" class="btn btn-primary submit-btn">Submit</button>
```

### Explanation:
- The `@keyframes buttonPress` animation scales the button slightly smaller when clicked and then returns it to its original size.
- The animation runs for `0.3s` with an `ease-in-out` transition to give it a smooth effect.

If you want the animation to trigger only when clicked, consider adding it dynamically using JavaScript:

```js
document.querySelector(".submit-btn").addEventListener("click", function () {
  this.style.animation = "buttonPress 0.3s ease-in-out";
});
```

Would you like to refine the animation further or add additional effects?