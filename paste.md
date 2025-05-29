In CSS, `z-index` is a property that controls the stack order of elements on a web page along the z-axis (depth). It determines which elements appear in front of or behind others. 

### How `z-index` Works:
- Elements with a higher `z-index` value appear above elements with a lower value.
- The `z-index` property only works for elements that have a `position` property set to `absolute`, `relative`, `fixed`, or `sticky`.
- If two elements have the same `z-index` value, the one appearing later in the HTML code will be on top.

### Example:
```css
.container {
  position: relative;
}

.box1 {
  position: absolute;
  top: 50px;
  left: 50px;
  width: 100px;
  height: 100px;
  background-color: blue;
  z-index: 2; /* Higher value, appears on top */
}

.box2 {
  position: absolute;
  top: 70px;
  left: 70px;
  width: 100px;
  height: 100px;
  background-color: red;
  z-index: 1; /* Lower value, appears below */
}
```

In this example, `.box1` will appear above `.box2` because its `z-index` is higher.

### Best Practices:
- Use `z-index` sparingly to avoid unnecessary complexity in layering elements.
- If layering issues occur, check the stacking context (parent elements can influence `z-index` behavior).
- Consider using `positioning` strategically instead of relying solely on `z-index`.

Would you like further clarification or more advanced examples?