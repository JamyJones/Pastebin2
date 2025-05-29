In JavaScript, native variables (like `let` or `const`) do not have built-in change listeners. However, you can achieve similar behavior using the following approaches:

### 1. Using `Object.defineProperty()` or `Proxy` for reactive variables

#### Using `Object.defineProperty()`

You can define a property with getter and setter, and inside the setter, place your listener logic:

```javascript
let _value;

const reactiveObject = {};
Object.defineProperty(reactiveObject, 'myVariable', {
  get() {
    return _value;
  },
  set(newValue) {
    _value = newValue;
    // Your change listener logic here
    console.log('Value changed:', newValue);
  },
  configurable: true,
  enumerable: true
});

// Usage:
reactiveObject.myVariable = 42; // Console: Value changed: 42
console.log(reactiveObject.myVariable); // 42
reactiveObject.myVariable = 100; // Console: Value changed: 100
```

#### Using `Proxy`

Proxies are more flexible and allow monitoring changes to objects or variables:

```javascript
let value = 0;

const handler = {
  set(target, property, newValue) {
    if (property === 'value') {
      console.log(`value changed from ${target[property]} to ${newValue}`);
    }
    target[property] = newValue;
    return true;
  }
};

const proxy = new Proxy({ value }, handler);

// Usage:
proxy.value = 10; // Console: value changed from 0 to 10
console.log(proxy.value); // 10
proxy.value = 20; // Console: value changed from 10 to 20
```

### 2. Using EventEmitter patterns or callback functions

Alternatively, if you want to track changes explicitly, you can implement a setter function that accepts callback functions:

```javascript
class ObservableVariable {
  constructor(initialValue) {
    this._value = initialValue;
    this.listeners = [];
  }

  set value(newValue) {
    if (this._value !== newValue) {
      this._value = newValue;
      this.notifyListeners(newValue);
    }
  }

  get value() {
    return this._value;
  }

  addListener(listener) {
    this.listeners.push(listener);
  }

  notifyListeners(newValue) {
    this.listeners.forEach(listener => listener(newValue));
  }
}

// Usage:
const obsVar = new ObservableVariable(0);
obsVar.addListener(val => console.log('Changed:', val));
obsVar.value = 5; // Console: Changed: 5
obsVar.value = 10; // Console: Changed: 10
```

---

### Summary:
- For tracking simple variable changes, using a `Proxy` or an accessor property (`get`/`set`) is effective.
- For more complex, multiple listeners, encapsulate the variable in a class with event callback management.
- Native variables (`let`, `const`) can't have change listeners directly; you need to wrap them in objects or proxies.

Let me know if you'd like a more specific implementation or have a particular use case!