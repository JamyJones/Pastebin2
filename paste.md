In CSS, the `z-index` property controls the vertical stacking order of elements that overlap each other on a webpage. It determines which element appears in front of or behind other overlapping elements.

### Key Points:
- `z-index` only works on elements that have a positioning context other than `static` (i.e., `position: relative`, `absolute`, `fixed`, or `sticky`).
- Higher `z-index` values appear in front of lower ones.
- The value can be positive, negative, or zero.

### Example Usage:

```css
/* Element with higher z-index will appear on top */
.element1 {
  position: absolute;
  top: 50px;
  left: 50px;
  z-index: 10;
  background-color: red;
  width: 100px;
  height: 100px;
}

.element2 {
  position: absolute;
  top: 80px;
  left: 80px;
  z-index: 5;
  background-color: blue;
  width: 100px;
  height: 100px;
}
```

In the example above:
- `.element1` has a `z-index` of `10`
- `.element2` has a `z-index` of `5`

Since `10 > 5`, `.element1` appears in front of `.element2`.

### Best Practices:
- Use meaningful `z-index` values to manage stacking order systematically.
- Avoid excessively high values to prevent confusion.
- Organize stacking contexts carefully, especially when dealing with nested elements.

### Stacking Context:
`z-index` creates a *stacking context.* A new stacking context is formed when an element has a position value other than `static` and a `z-index` value (or certain other CSS properties), affecting how child elements are stacked relative to other elements.

---

**Summary:**
```plaintext
z-index: controls the stack order of overlapping elements.
It only works on positioned elements.
Higher values appear on top.
```

If you need further clarification or examples, feel free to ask!