In ES6 modules, each module has its own scope, and there's no truly *global* variable shared across modules in the traditional sense. However, you can achieve shared state by exporting variables or objects that are mutable, which can then be imported and modified across different modules.

Here's a common and **standard** approach:

### 1. Create a singleton state object

You can define an *object* containing the array and export it. Since objects are mutable, other modules can import and modify the array directly.

```js
// state.js
export const globalState = {
  myArray: []
};
```

### 2. Import and modify the array in other modules

```js
// moduleA.js
import { globalState } from './state.js';

// Push to the array
globalState.myArray.push('item1');

console.log(globalState.myArray); // ['item1']
```

```js
// moduleB.js
import { globalState } from './state.js';

console.log(globalState.myArray); // ['item1']

// Clear the array
globalState.myArray.length = 0;

console.log(globalState.myArray); // []
```

---

### Summary of best practices:
- Export an object (or a class instance).
- Mutate the internal properties (like an array) directly.
- All modules that import the object share the same reference, maintaining a shared state.

### Additional note:
Be cautious with shared state—consider better state management approaches if your application grows complex (e.g., using state management libraries or context in frameworks like React).

---

**Full example:**

```js
// state.js
export const globalState = {
  myArray: []
};
```

```js
// app.js
import { globalState } from './state.js';

globalState.myArray.push('Item 1');
console.log(globalState.myArray); // ['Item 1']

// Later, in another module
import { globalState } from './state.js';

globalState.myArray.push('Item 2');
console.log(globalState.myArray); // ['Item 1', 'Item 2']
```

This pattern ensures that all modules are working with the same shared mutable object.

---

If you need a *more encapsulated* approach, you can export getter/setter functions, but the above pattern is most straightforward for shared mutable state in ES6 modules.