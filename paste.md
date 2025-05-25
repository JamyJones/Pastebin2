To convert an array of objects into a JSON object in JavaScript, you can use the `JSON.stringify()` method. This method converts a JavaScript object or value to a JSON string. Here's a simple example:

### Example

Suppose you have the following array of objects:

```javascript
const arrayOfObjects = [
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" },
    { id: 3, name: "Charlie" }
];
```

You can convert this array into a JSON string like this:

```javascript
const jsonObject = JSON.stringify(arrayOfObjects);
console.log(jsonObject);
```

### Output

The output will be a JSON string representation of the array:

```json
'[{"id":1,"name":"Alice"},{"id":2,"name":"Bob"},{"id":3,"name":"Charlie"}]'
```

### Converting Back to JavaScript Object

If you need to convert the JSON string back into a JavaScript object, you can use `JSON.parse()`:

```javascript
const parsedObject = JSON.parse(jsonObject);
console.log(parsedObject);
```

This will give you back the original array of objects.

### Summary

- Use `JSON.stringify(array)` to convert an array of objects to a JSON string.
- Use `JSON.parse(jsonString)` to convert a JSON string back to a JavaScript object.