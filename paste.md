The issue you're facing occurs because when you define `pages_obj` in the object using an arrow function, it doesn't execute immediately—it remains as a function reference. This means that when you access `pages_obj`, you're actually retrieving the function itself, rather than its returned value.

### Solution:
You need to **invoke** the function to get the expected result when accessing `pages_obj`. Here’s how you can structure it:

```javascript
resolve({
  'arr_students2': arr_students2,
  'pages_obj': (() => {
    let pages_obj = {}; // Define pages_obj properly
    pages_obj["length"] = page_count;
    return pages_obj;
  })() // Immediately Invoked Function Expression (IIFE)
});
```

### Explanation:
1. **IIFE (Immediately Invoked Function Expression)**: Wrapping the arrow function inside `()` and executing it immediately ensures that `pages_obj` is **not a function**, but an actual object.
2. **Proper Initialization**: Defining `pages_obj` inside the function scope makes sure that it's manipulated correctly.

By applying this approach, when you access `pages_obj`, you'll get an object instead of a function reference.

Would you like additional explanations or a different approach?