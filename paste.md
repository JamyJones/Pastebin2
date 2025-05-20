Object destructuring in JavaScript is a powerful feature that allows you to extract properties from objects and assign them to variables in a concise and readable way. It is commonly used to simplify code, especially when working with APIs, configurations, and nested data structures.

### Basic Object Destructuring
Here's a simple example:

```javascript
const user = {
    name: "Alice",
    age: 25,
    location: "New York"
};

// Extract properties into variables
const { name, age, location } = user;

console.log(name); // "Alice"
console.log(age); // 25
console.log(location); // "New York"
```

### Default Values
You can set default values for properties that might be `undefined`:

```javascript
const person = { name: "Bob" };

const { name, age = 30 } = person;

console.log(age); // 30 (default value)
```

### Renaming Variables
You can rename the extracted variables using a colon (`:`):

```javascript
const employee = {
    fullName: "Charlie Smith",
    position: "Developer"
};

const { fullName: name, position: jobTitle } = employee;

console.log(name); // "Charlie Smith"
console.log(jobTitle); // "Developer"
```

### Nested Object Destructuring
Destructuring works with nested objects too:

```javascript
const company = {
    name: "TechCorp",
    address: {
        city: "San Francisco",
        country: "USA"
    }
};

const { name, address: { city, country } } = company;

console.log(city); // "San Francisco"
console.log(country); // "USA"
```

### Using Destructuring in Function Parameters
Object destructuring is useful in function parameters to directly extract needed values:

```javascript
function displayUser({ name, age }) {
    console.log(`${name} is ${age} years old.`);
}

const userData = { name: "Diana", age: 28 };

displayUser(userData); // "Diana is 28 years old."
```

### Best Practices
- Use destructuring to improve code readability and maintainability.
- Provide default values when necessary to prevent `undefined` errors.
- Rename variables where necessary to keep naming consistent.

Destructuring is widely used in modern JavaScript development, especially in React applications, API handling, and more. Would you like me to demonstrate advanced use cases or integrations with frameworks?