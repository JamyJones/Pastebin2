In ES6 JavaScript modules, you can create a global variable by exporting it from a module. To achieve a variable that points to an array and can be modified (e.g., pushed to or cleared), you can follow these steps:

1. **Create a module**: Define your variable and export it.
2. **Modify the variable**: Use functions to manipulate the array.

Here's an example:

### myModule.js
```javascript
// Create a global variable that points to an array
let globalArray = [];

// Function to push a value to the array
export function pushToArray(value) {
    globalArray.push(value);
}

// Function to clear the array
export function clearArray() {
    globalArray = [];
}

// Function to get the current state of the array
export function getArray() {
    return globalArray;
}
```

### main.js
```javascript
import { pushToArray, clearArray, getArray } from './myModule.js';

// Push values to the global array
pushToArray(1);
pushToArray(2);
pushToArray(3);

console.log(getArray()); // Output: [1, 2, 3]

// Clear the array
clearArray();

console.log(getArray()); // Output: []
```

### Explanation:
- In `myModule.js`, we define a variable `globalArray` and export functions to manipulate it.
- The `pushToArray` function allows you to add elements to the array.
- The `clearArray` function resets the array to an empty state.
- The `getArray` function returns the current state of the array.

This way, you can maintain a global variable that can be modified across different modules.