The issue you're encountering is due to the fact that you're defining `pages_obj` as an arrow function rather than as an object. When you access `pages_obj`, you're getting the function definition instead of the object you expect.

Here's a breakdown of what's happening:

1. You are defining `pages_obj` as a function: `()=>{pages_obj["length"]=page_count;return pages_obj;}`.
2. When you try to access `pages_obj`, you are actually accessing the function itself, not the result of calling that function.

To fix this, you should define `pages_obj` as an object directly, or if you want to keep it as a function, you need to call it to get the object. Here are two possible solutions:

### Solution 1: Define `pages_obj` as an object

If you want `pages_obj` to be an object that you can modify, you can define it directly:

```javascript
const pages_obj = {
    length: page_count
};

resolve({'arr_students2': arr_students2, 'pages_obj': pages_obj});
```

### Solution 2: Keep it as a function but call it

If you want to keep the function definition, you need to call it to get the object:

```javascript
const pages_obj = () => {
    const obj = {};
    obj["length"] = page_count;
    return obj;
};

resolve({'arr_students2': arr_students2, 'pages_obj': pages_obj()});
```

In this second solution, `pages_obj()` is called, and it returns the object with the `length` property set to `page_count`. 

Choose the solution that best fits your use case!