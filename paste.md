Yes, in JavaScript, you can have an asynchronous function that uses `await` without blocking the main thread. The `await` keyword is used to pause the execution of an `async` function until a Promise is resolved, but it does not block the main thread. Instead, it allows other operations to continue running while waiting for the Promise to resolve.

Here's a simple example to illustrate this:

```javascript
async function exampleFunction() {
    console.log("Start of the function");

    // Simulate an asynchronous task
    const result = await new Promise((resolve) => {
        setTimeout(() => {
            resolve("Task completed");
        }, 2000); // Simulates a 2-second task
    });

    console.log(result); // This will log after the Promise is resolved
    console.log("End of the function");
}

console.log("Before calling exampleFunction");
exampleFunction();
console.log("After calling exampleFunction");
```

### Explanation:
1. When `exampleFunction` is called, it logs "Before calling exampleFunction".
2. The function starts executing and logs "Start of the function".
3. The `await` keyword pauses the execution of `exampleFunction` until the Promise resolves, but it does not block the main thread. This means that the code after the `await` can still run.
4. While waiting for the Promise to resolve, the main thread continues executing and logs "After calling exampleFunction".
5. After 2 seconds, the Promise resolves, and the execution of `exampleFunction` resumes, logging "Task completed" and "End of the function".

This demonstrates that while `await` pauses the execution of the async function, it does not block the main thread, allowing other code to run concurrently.