Yes, you can observe the order in which JavaScript functions are executed using browser developer tools. Here are some effective methods:

---

### 1. **Using the Call Stack in the Debugger**

**How**:
- Set breakpoints in your code where you want to observe execution.
- When the code hits a breakpoint, the debugger will pause, and the **Call Stack** panel shows the sequence of function calls leading to the current point.

**Steps**:
1. Open DevTools (Chrome DevTools, Firefox DevTools, etc.).
2. Navigate to the **Sources** (Chrome) or **Debugger** (Firefox) tab.
3. Set breakpoints on functions or lines of code.
4. Trigger the execution path.
5. When paused, look at the **Call Stack** pane to see the order of function calls.

**Example**:

```js
function a() {
    b();
}
function b() {
    c();
}
function c() {
    debugger; // Pauses here
}

// Call the initial function
a();
```

When execution hits `debugger;`, the call stack will show:
```
- c()
- b()
- a()
```

---

### 2. **Using `console.trace()`**

- You can insert `console.trace()` inside functions to log the call stack at that point.

```js
function a() {
    console.trace('Trace from a');
    b();
}
function b() {
    console.trace('Trace from b');
    c();
}
function c() {
    console.trace('Trace from c');
}

a();
```

**Result**:
- Each `console.trace()` outputs the stack trace in the console, indicating the sequence of calls leading to that function.

---

### 3. **Monitoring with Event Listeners or Function Wrapping**

- For asynchronous or complex flows, you can wrap functions with logging:

```js
function logExecution(fn, name) {
    return function(...args) {
        console.log(`Executing ${name}`);
        return fn.apply(this, args);
    };
}

const a = logExecution(function() {
    b();
}, 'a');

const b = logExecution(function() {
    c();
}, 'b');

const c = logExecution(function() {
    console.log('In c');
}, 'c');

a();
```

This logs the order of execution explicitly as your code runs.

---

### 4. **Using Performance Profilers**

- Use the **Performance** tab in Chrome DevTools to record runtime and view **Call Trees**.
- Start recording, perform actions, then stop recording.
- The **Call Tree** shows the sequence and duration of function calls.

---

### Summary:
- **Breakpoints + Call Stack**: Visualizes current function call order.
- **`console.trace()`**: Logs call stacks at specific points.
- **Profilers**: Capture the full execution flow over an interval.
- **Wrapper functions**: For detailed logging in complex flows.

---

Would you like a specific example or detailed steps for a certain scenario?