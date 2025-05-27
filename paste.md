In JavaScript, when you resolve a `Promise`, you can pass any data you want — including objects, arrays, or multiple values. Typically, if you want to pass multiple pieces of data, you wrap them in an object or array.

### Common approach: Wrap multiple data items in an object

```js
function foo() {
  return new Promise(function(resolve, reject) {
    const data1 = [1, 2, 3];
    const data2 = { key: 'value' };
    // Pass an object containing multiple data items
    resolve({ data1, data2 });
  });
}
```

### Consuming the Promise with `await`

```js
async function main() {
  const { data1, data2 } = await foo();
  console.log(data1); // [1, 2, 3]
  console.log(data2); // { key: 'value' }
}

main();
```

---

### Alternative: Pass an array of multiple values

```js
function foo() {
  return new Promise(function(resolve, reject) {
    const arrayData = [1, 2, 3];
    const objectData = { key: 'value' };
    resolve([arrayData, objectData]);
  });
}
```

```js
async function main() {
  const [arrayData, objectData] = await foo();
  console.log(arrayData); // [1, 2, 3]
  console.log(objectData); // { key: 'value' }
}

main();
```

---

### Summary

- Use `resolve()` with an **object** or **array** containing multiple data pieces.
- When consuming, **destructure** the resolved value accordingly.

**Note:** For clarity and maintainability, using an object with descriptive keys is preferred, especially when passing multiple data items.