To convert an array of objects into a JSON object, you need to decide how to structure the resulting JSON. Common approaches include transforming the array into an object where keys are derived from some property of each object, or wrapping the array into a property of an object.

### Example 1: Wrap array in an object property
If you simply want to encapsulate the array inside a JSON object, you can do:

```js
const arrayOfObjects = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' }
];

const jsonObject = {
  data: arrayOfObjects
};

console.log(JSON.stringify(jsonObject, null, 2));
```
**Output:**
```json
{
  "data": [
    { "id": 1, "name": "Alice" },
    { "id": 2, "name": "Bob" }
  ]
}
```

### Example 2: Convert array to an object with keys
If you want to create a JSON object where each key is derived from a property within each object (for instance, `id`), do:

```js
const arrayOfObjects = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' }
];

const jsonObject = arrayOfObjects.reduce((acc, obj) => {
  acc[obj.id] = obj;
  return acc;
}, {});

console.log(JSON.stringify(jsonObject, null, 2));
```
**Output:**
```json
{
  "1": { "id": 1, "name": "Alice" },
  "2": { "id": 2, "name": "Bob" }
}
```

### Summary:
- Use `JSON.stringify()` to convert JavaScript objects or arrays into JSON strings.
- Structure the object as needed, e.g., wrapping the array inside a property or transforming into key-value pairs.

**Note:** JSON is a string format, but here the focus is on creating the JavaScript object structure that will then be serialized into JSON.

---

If you have specific structure requirements or a particular shape for the output JSON, please specify, and I can tailor the solution accordingly.