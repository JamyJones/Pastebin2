Your Bootstrap tab functionality isn't working because you're using `data-toggle="tab"` instead of the correct Bootstrap 5 syntax. Bootstrap 5 removed jQuery dependency, and now uses `data-bs-toggle` instead of `data-toggle`. 

### **Fix:**
Update your button elements like this:

```html
<button type="button" class="nav-link active" id="login-tab" data-bs-toggle="tab" data-bs-target="#login" role="tab" aria-controls="login" aria-selected="true">Login</button>

<button type="button" class="nav-link" id="signup-tab" data-bs-toggle="tab" data-bs-target="#signup" role="tab" aria-controls="signup" aria-selected="false">Sign Up</button>
```

### **Explanation:**
- `data-bs-toggle="tab"` is the correct attribute in Bootstrap 5.
- `data-bs-target="#signup"` correctly links the tab to its content.
- The `data-toggle` attribute is from Bootstrap 4 and won't work in Bootstrap 5.

Try this fix, and your tabs should work smoothly. Let me know if you need further troubleshooting!
