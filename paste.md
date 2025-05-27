In JavaScript, arrow functions provide a concise syntax to define functions. To return a value explicitly from an arrow function, there are two common approaches depending on the function's complexity.

### 1. **Implicit Return (Single Expression)**

If the arrow function contains only a single expression, you can omit the curly braces and `return` keyword. The value of the expression will be returned automatically.

```javascript
const add = (a, b) => a + b;

console.log(add(2, 3)); // Output: 5
```

### 2. **Explicit Return (Multiple Statements or Complex Logic)**

If the function body contains multiple statements, you need to wrap the body in curly braces and include an explicit `return` statement.

```javascript
const multiply = (a, b) => {
  const result = a * b;
  return result;
};

console.log(multiply(4, 5)); // Output: 20
```

### Summary:
- **Single expression:** `const func = () => expression;`
- **Multiple statements:** 
  ```javascript
  const func = () => {
    // multiple statements
    return value;
  };
  ```

Let me know if you'd like examples with specific use cases!