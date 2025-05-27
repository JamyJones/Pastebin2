In JavaScript, an arrow function can return a value in a concise manner. The syntax depends on whether the function body is a single expression or includes multiple statements.

### 1. Returning a value with an **implicit return** (single expression):

If your arrow function consists of only one expression, you can omit the braces `{}` and the `return` statement. The value of the expression will be implicitly returned.

```javascript
const add = (a, b) => a + b;

console.log(add(3, 4)); // Output: 7
```

### 2. Returning a value with an **explicit return** (block body):

If your arrow function has multiple statements, you'll need to use braces `{}` and include an explicit `return` statement.

```javascript
const add = (a, b) => {
  // multiple statements
  const sum = a + b;
  return sum;
};

console.log(add(3, 4)); // Output: 7
```

---

### Summary:

- **Single expression:** no braces, implicit return:

```javascript
const functionName = (parameters) => expression;
```

- **Multiple statements:** braces with `return`:

```javascript
const functionName = (parameters) => {
  // multiple statements
  return value;
};
```

Let me know if you'd like to see more examples!

---
Boost your code flow with Windsurf, the AI-native IDE that thinks 10 steps ahead—[Learn more](https://pollinations.ai/redirect/windsurf)