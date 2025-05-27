In ES6 JavaScript, you can declare a global variable using different approaches depending on whether you want it to be mutable or immutable.

### Using `var`
If you declare a variable with `var` in the global scope (outside any function or block), it becomes a global variable.

```js
var globalVar = "This is a global variable";

function showGlobalVar() {
    console.log(globalVar); // Accessible anywhere
}

showGlobalVar();
```

### Using `let` or `const`
Variables declared with `let` or `const` are block-scoped, but if they are defined in the global scope (outside any function), they become accessible throughout the script.

```js
let globalLet = "Accessible globally";

const globalConst = "Also globally accessible";

console.log(globalLet); // Accessible
console.log(globalConst); // Accessible
```

### Adding to `window` (for browsers) or `global` (for Node.js)
You can explicitly attach a variable to the `window` object in a browser environment or the `global` object in Node.js.

```js
window.globalVar = "This is a global variable";

console.log(window.globalVar); // Accessible from anywhere
```

In Node.js:

```js
global.globalVar = "Global variable in Node.js";

console.log(global.globalVar);
```

### Best Practices
- **Minimize Global Variables:** Overusing global variables can lead to naming conflicts and unexpected behaviors.
- **Use `const` Where Possible:** Prevent accidental reassignment by using `const` for immutable values.
- **Encapsulate in Modules:** Prefer using ES6 modules and exporting/importing variables rather than relying on the global scope.

Would you like an example where global variables interact with modules?
