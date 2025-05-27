In ES6 JavaScript, you can create a global variable that points to an array and can be modified (e.g., pushed to or cleared) by declaring it outside of any function or block scope. Here's how you can do it:

1. **Declare the global variable**: You can declare the variable using `let`, `const`, or `var`. However, using `let` or `const` is recommended for block scoping.

2. **Modify the array**: You can use methods like `push()` to add elements to the array and `length = 0` to clear it.

Here's an example:

```javascript
// Declare a global variable
let globalArray = [];

// Function to add an element to the array
function addElement(element) {
    globalArray.push(element);
}

// Function to clear the array
function clearArray() {
    globalArray.length = 0; // or globalArray = [];
}

// Example usage
addElement(1);
addElement(2);
console.log(globalArray); // Output: [1, 2]

clearArray();
console.log(globalArray); // Output: []
```

In this example:
- `globalArray` is a global variable that can be accessed and modified from anywhere in your code.
- The `addElement` function allows you to add elements to the array.
- The `clearArray` function clears the array by setting its length to 0. 

You can call these functions from anywhere in your code to modify the `globalArray`.