You're seeing a function definition instead of its returned value because when you assign an arrow function to `'pages_obj'`, you're storing the function itself inside the object, not its execution result. 

When you later try to access `'pages_obj'`, you're retrieving the function definition—not executing it. To resolve this, you need to call the function explicitly when you need its result, like this:

```javascript
const resolvedValue = resolve({
    'arr_students2': arr_students2,
    'pages_obj': () => {
        const pages_obj = {}; // Declare the object
        pages_obj["length"] = page_count;
        return pages_obj;
    }
});

// Access the value by calling the function
console.log(resolvedValue.pages_obj()); // This will return the expected object
```

### Best Practice:
- **Avoid modifying undefined objects**: In your original code, `pages_obj["length"]=page_count;` assumes `pages_obj` is already defined. If it isn't, you'll encounter an error.
- **Use function execution explicitly**: If an object property holds a function, you need to invoke it manually when accessing its value.
- **Consider direct object assignment**: If you don’t need dynamic execution, assign the object directly instead of wrapping it inside a function.

Let me know if you need further clarification or refinements. 🚀
