In ES6 modules, **each module has its own scope**, so you can't directly create true "global" variables that are accessible across modules without explicit export-import mechanisms. However, you can achieve shared state (like a global variable) by exporting an **object** or **array** that is mutable, and then importing and modifying it in other modules. 

### Recommended Approach: Use a shared mutable object or array

Here's how to implement a shared variable, such as an array that can be pushed to or cleared, using module exports.

---

### Example

#### `sharedState.js`

```js
// Export a mutable array
export const sharedArray = [];
```

---

#### Usage in other modules:

```js
import { sharedArray } from './sharedState.js';

// Add an item
sharedArray.push('new item');

// Clear the array
sharedArray.length = 0;

// Log current state
console.log(sharedArray);
```

---

### Explanation

- Since `sharedArray` is **imported by reference**, any modifications to it (push, splice, etc.) in one module will be visible in all modules that import it.
- You can also use an object if you want to store multiple state variables in a structured way:

```js
// `sharedState.js`
export const state = {
  myArray: [],
  someValue: null,
};
```

```js
// in other modules
import { state } from './sharedState.js';

state.myArray.push(1);
state.someValue = 'updated';
```

---

### Important Points:
- Avoid polluting the global scope; **use module exports** for shared state.
- Remember, **mutations on shared objects are reflected everywhere** because of reference semantics.
- If you need to **trigger reactions** on state changes, consider integrating with reactive frameworks or adding explicit update functions.

---

Would you like an example of how to encapsulate this in a class or use a singleton pattern for more complex shared state management?