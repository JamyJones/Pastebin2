In JavaScript, you can convert a string to a number using several methods depending on the type of conversion needed. Here are the most common techniques:

### 1. Using `Number()` 
This method converts a string into a number, including decimals.

```javascript
let num = Number("42"); // Outputs: 42
let decimalNum = Number("3.14"); // Outputs: 3.14
```

### 2. Using `parseInt()` (for integers)
This function parses a string and returns an integer.

```javascript
let intNum = parseInt("42"); // Outputs: 42
let intNumWithText = parseInt("42px"); // Outputs: 42 (ignores non-numeric characters)
```

### 3. Using `parseFloat()` (for floating-point numbers)
This function is similar to `parseInt()`, but retains decimals.

```javascript
let floatNum = parseFloat("3.14"); // Outputs: 3.14
```

### 4. Using the `+` Unary Operator
A shorthand method that quickly converts a string to a number.

```javascript
let shortNum = +"42"; // Outputs: 42
let shortFloat = +"3.14"; // Outputs: 3.14
```

### 5. Using `Math.floor()` or `Math.round()` (for rounding)
Useful when rounding is required.

```javascript
let roundedNum = Math.floor("3.99"); // Outputs: 3
let roundedNum2 = Math.round("3.99"); // Outputs: 4
```

### Best Practices:
- Always validate input before conversion to avoid unexpected results.
- Use `Number()` when you need full numeric conversion, but avoid it for strings with non-numeric characters.
- Prefer `parseInt()` or `parseFloat()` when handling text-based numbers.
- Be cautious with `+` unary operator as it may cause unintended coercion.

Would you like further clarification on any of these methods?