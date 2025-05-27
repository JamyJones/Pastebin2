In JavaScript, arrow functions provide a concise way to write functions. To return a value directly from an arrow function, you can use either:

1. **Implicit return (for single expression functions):**

When the function body is a single expression, omit the curly braces `{}` and the `return` statement. The expression's result is automatically returned.

```javascript
const square = x => x * x;

console.log(square(5)); // Output: 25
```

2. **Explicit return (if you need multiple statements):**

Use curly braces `{}` and include a `return` statement.

```javascript
const sum = (a, b) => {
  return a + b;
};

console.log(sum(3, 4)); // Output: 7
```

**Summary:**

- Use `x => expression` for implicit return.
- Use `(args) => { ... }` with `return` inside for multiple statements.

Would you like an example involving returning a value inside a more complex arrow function?

---
Boost your coding flow with [Windsurf](https://pollinations.ai/redirect/windsurf), the AI-native IDE that writes and refines your arrow functions effortlessly.