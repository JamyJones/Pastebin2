Yes, you can see the order in which JavaScript functions are executed using browser developer tools, specifically with the **Call Stack** and **Debugger** features. Here's how to do it professionally:

### 1. **Using Breakpoints and Call Stack**

**Steps:**

1. **Open DevTools:**
   - In Chrome/Edge: Right-click on the webpage → Inspect or press `F12` or `Ctrl+Shift+I`.

2. **Navigate to Sources tab (Chrome) / Debugger tab (Firefox):**
   - This is where you can set breakpoints and see the call stack.

3. **Set Breakpoints:**
   - Find the JavaScript file or inline script in the **Sources** panel.
   - Click on the line number where you want to pause execution (e.g., inside a function).

4. **Trigger the code execution:**
   - Interact with your webpage or refresh to hit the breakpoint.

5. **Examine the Call Stack:**
   - When paused, look at the **Call Stack** panel.
   - The call stack shows the sequence of function calls leading to the current point.

**Example:**

```js
function a() {
    b();
}

function b() {
    c();
}

function c() {
    debugger; // You can also add a breakpoint here
    // some code
}

a();
```

- When hitting the `debugger;` line, the call stack might look like:

```
→ c()
  b()
  a()
```

which shows the order of calls.

---

### 2. **Using `console.trace()`**

You can programmatically log the call stack at any point:

```js
function a() {
    console.trace("Trace from function a");
    b();
}

function b() {
    console.trace("Trace from function b");
    c();
}

function c() {
    console.trace("Trace from function c");
}

a();
```

This will output the call stack in the console whenever the function is invoked, showing the sequence of calls leading to it.

---

### 3. **Profiling with Performance Tab**

For a more comprehensive view:

1. Go to the **Performance** tab.
2. Click **Record**.
3. Interact with the page or trigger your functions.
4. Stop recording.
5. Analyze the **Main Thread activity**, which includes function call sequences and timings.

---

### **Summary**

- Use **breakpoints** and the **Call Stack** panel for precise, step-by-step debugging.
- Use `console.trace()` for quick insights into how functions are called.
- Use the **Performance** profiling tools for high-level sequence and timing analysis.

---

**Note:** If you want to trace asynchronous functions or promises, the call stack might be asynchronous, so be aware that certain sequences might be reconstructed differently. Use async call stack options (`Pause on exceptions`, etc.) to better visualize such flows.