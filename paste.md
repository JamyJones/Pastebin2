Yes, in JavaScript, you can listen for changes to a variable using various methods. One common approach is to use a getter and setter with an object or to use a Proxy. Here are a couple of methods to achieve this:

### Method 1: Using Getters and Setters

You can define an object with a property that uses a getter and setter to listen for changes:

```javascript
const obj = {
    _value: 0, // private variable

    get value() {
        return this._value;
    },

    set value(newValue) {
        console.log(`Value changed from ${this._value} to ${newValue}`);
        this._value = newValue;
    }
};

// Usage
obj.value = 10; // Logs: Value changed from 0 to 10
console.log(obj.value); // Outputs: 10
```

### Method 2: Using Proxy

You can also use a `Proxy` to intercept changes to an object's properties:

```javascript
const target = {
    value: 0
};

const handler = {
    set(obj, prop, value) {
        if (prop === 'value') {
            console.log(`Value changed from ${obj[prop]} to ${value}`);
        }
        obj[prop] = value;
        return true; // Indicate success
    }
};

const proxy = new Proxy(target, handler);

// Usage
proxy.value = 10; // Logs: Value changed from 0 to 10
console.log(proxy.value); // Outputs: 10
```

### Summary

Both methods allow you to listen for changes to a variable. The first method is straightforward and works well for simple cases, while the second method using `Proxy` is more flexible and can be used for more complex scenarios. Choose the one that best fits your needs!