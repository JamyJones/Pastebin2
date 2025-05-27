In ES6 JavaScript, to create a global variable that can be modified like an array (e.g., push to it or clear it), the common practice is to declare a variable with `let` or `const` at the global scope.

### Best Practice:
- Use `const` when you want the reference to the array to stay constant, but still allow modifying the array itself (push, pop, clear, etc.).
- Use `let` if you expect to reassign the variable itself later.

### Example:

```js
// Declare a global array with const (reference won't change)
const globalArray = [];

// Push elements into the array
globalArray.push(1);
globalArray.push(2);
console.log(globalArray); // [1, 2]

// Clear the array
globalArray.length = 0; // Clears the array
console.log(globalArray); // []
```

### Important notes:
- Declaring with `const` **does not** prevent modification of the array’s contents, only the reassignment of the variable. 
- If you want to prevent reassigning the array, declare it with `const`.
- To clear the array, setting its `length` to 0 is an efficient way.

### Example (wrapping in a module for better practice):

In modern development, global variables are generally discouraged, but if needed, they can be managed via a module pattern.

```js
// globals.js
export const globalArray = [];
```

```js
// main.js
import { globalArray } from './globals.js';

globalArray.push('item1');
console.log(globalArray); // ['item1']

// To clear
globalArray.length = 0;
console.log(globalArray); // []
```

This way, you control global state properly with modules.

---

**Summary:**
- Use `const globalArray = []` at the global scope.
- Modify it with `.push()`, `.pop()` or clearing (`array.length = 0`) as needed.
- Avoid reassigning the variable unless necessary.

Would you like an example incorporating encapsulation or module pattern for managing global state?