You’re encountering this error because the classList.add() method only accepts individual class names as separate arguments, not a single string containing multiple classes separated by spaces.

Incorrect usage:
```js
element.classList.add('rounded-circular m-0'); // ❌ This will throw a DOMException
```

Correct usage:
```js
element.classList.add('rounded-circular', 'm-0'); // ✅ This adds both classes properly
```

**Best Practice:**  
Always pass each class name as a separate argument to classList.add(). If you have a string of classes (e.g., from a template or variable), use .split(' ') to separate them:

```js
const classes = 'rounded-circular m-0';
element.classList.add(...classes.split(' '));
```

This approach ensures that each class is added individually, preventing the DOMException. Let me know if you need further clarification or examples.