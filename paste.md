In JavaScript, you can pass an arrow function's value directly within an object by defining the function as a property of the object. Here's an example to illustrate this:

```javascript
const myObject = {
    myFunction: () => {
        return "Hello, World!";
    }
};

// Calling the arrow function
console.log(myObject.myFunction()); // Output: Hello, World!
```

In this example, `myFunction` is an arrow function defined as a property of `myObject`. When you call `myObject.myFunction()`, it executes the arrow function and returns the string "Hello, World!". 

If you want to pass parameters to the arrow function, you can do so as follows:

```javascript
const myObject = {
    greet: (name) => {
        return `Hello, ${name}!`;
    }
};

// Calling the arrow function with a parameter
console.log(myObject.greet("Alice")); // Output: Hello, Alice!
```

Here, the `greet` function takes a `name` parameter and returns a greeting message.