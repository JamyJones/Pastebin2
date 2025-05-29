Yes, in JavaScript, there is no built-in way to directly listen for changes to a primitive variable. However, there are several approaches to achieve this behavior:

### 1. **Using a Getter and Setter with Object**
One common approach is to use an object and define getters and setters with `Object.defineProperty`:

```javascript
const obj = { value: 0 };

Object.defineProperty(obj, "value", {
  get() {
    return this._value;
  },
  set(newValue) {
    console.log(`Value changed to: ${newValue}`);
    this._value = newValue;
  }
});

obj.value = 42; // Logs: Value changed to: 42
```

### 2. **Using Proxy API**
A more modern approach uses `Proxy` to listen for changes:

```javascript
const handler = {
  set(target, property, value) {
    console.log(`Value changed to: ${value}`);
    target[property] = value;
    return true;
  }
};

const obj = new Proxy({ value: 0 }, handler);

obj.value = 100; // Logs: Value changed to: 100
```

### 3. **Using EventEmitter (Node.js)**
If you're working in a Node.js environment, you can use the `EventEmitter` module:

```javascript
const EventEmitter = require("events");
class ValueObserver extends EventEmitter {
  constructor() {
    super();
    this._value = 0;
  }

  set value(newValue) {
    this._value = newValue;
    this.emit("change", newValue);
  }

  get value() {
    return this._value;
  }
}

const observer = new ValueObserver();
observer.on("change", (val) => console.log(`Value changed to: ${val}`));

observer.value = 200; // Logs: Value changed to: 200
```

### Best Practices:
- Use `Proxy` for a cleaner and more scalable solution.
- If working with Node.js, prefer `EventEmitter` for event-driven architecture.
- If working with React, use state management libraries like Redux or useState/useEffect hooks instead.

Would you like a more advanced example or an application-based scenario?