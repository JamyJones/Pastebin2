Certainly! Below is a CSS animation class that you can apply to your button when submitting a form. This animation gives a subtle "loading" effect by making the button scale slightly and change opacity.

### CSS Code:
```css
@keyframes buttonLoading {
    0% {
        transform: scale(1);
        opacity: 1;
    }
    50% {
        transform: scale(0.95);
        opacity: 0.7;
    }
    100% {
        transform: scale(1);
        opacity: 1;
    }
}

.button-submit {
    background-color: #007bff;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}

.button-submit:active {
    animation: buttonLoading 1s infinite;
}
```
### Explanation:
- The `@keyframes buttonLoading` defines the animation steps.
- The button shrinks (`scale(0.95)`) and becomes slightly transparent (`opacity: 0.7`) at 50% of the animation.
- The button returns to normal (`scale(1)`, `opacity: 1`) by the end of the animation cycle.
- When the button is clicked (`:active`), the animation runs infinitely until released.

This ensures a sleek visual cue that the form is being submitted. Let me know if you need further adjustments!