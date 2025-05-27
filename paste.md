In ES6 (ECMAScript 2015) JavaScript, you can create a global variable by declaring it in the global scope. However, it's important to note that using global variables is generally discouraged due to potential conflicts and difficulties in maintaining code. If you still need to create a global variable, here are a few ways to do it:

### 1. Using `var` in the global scope

If you declare a variable with `var` outside of any function or block, it becomes a global variable:

```javascript
var globalVar = "I am a global variable";

function showGlobalVar() {
    console.log(globalVar);
}

showGlobalVar(); // Output: I am a global variable
```

### 2. Using `window` object in browsers

In a browser environment, you can attach a variable to the `window` object to make it global:

```javascript
window.globalVar = "I am a global variable";

function showGlobalVar() {
    console.log(window.globalVar);
}

showGlobalVar(); // Output: I am a global variable
```

### 3. Using `let` or `const` in the global scope

Variables declared with `let` or `const` at the top level of a module are not added to the global object. However, if you want to create a global variable in a script that is not a module, you can still use `let` or `const` in the global scope:

```javascript
let globalVar = "I am a global variable"; // This will not be on the window object in a module

function showGlobalVar() {
    console.log(globalVar);
}

showGlobalVar(); // Output: I am a global variable
```

### 4. Using a module

If you are using ES6 modules, you can export a variable and import it wherever needed, which is a better practice than using global variables:

```javascript
// global.js
export const globalVar = "I am a global variable";

// main.js
import { globalVar } from './global.js';

function showGlobalVar() {
    console.log(globalVar);
}

showGlobalVar(); // Output: I am a global variable
```

### Conclusion

While you can create global variables in ES6, it's often better to limit their use and consider alternatives like modules or encapsulating variables within functions or classes to avoid potential issues with variable scope and conflicts.