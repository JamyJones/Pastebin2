In CSS, `z-index` is a property used to control the stacking order of overlapping elements on a webpage. It determines which element appears in front of or behind other elements when they overlap.

### Key Points:
- **Applicability:** `z-index` only works on elements positioned with a non-static position value (`relative`, `absolute`, `fixed`, or `sticky`).
- **Values:** It accepts integer values (positive, negative, or zero).
  - Higher `z-index` values appear in front of lower ones.
- **Default:** Elements have a default `z-index` of `auto`, which means they stack according to document order unless specified otherwise.

### Example:
```css
div {
  position: absolute;
}

/* Element A */
#elementA {
  top: 50px;
  left: 50px;
  background-color: red;
  z-index: 1; /* Behind elementB */
}

/* Element B */
#elementB {
  top: 70px;
  left: 70px;
  background-color: blue;
  z-index: 2; /* In front of elementA */
}
```

### Visual Representation:
- `#elementA` appears behind `#elementB` because it has a lower `z-index`.
- Increasing the `z-index` brings the element to the front.

### Best Practices:
- Use relative, absolute, fixed, or sticky positioning when manipulating `z-index`.
- Keep stacking contexts small; overly complex stacking can become difficult to manage.
- Be cautious with `z-index` values; use meaningful increments to improve readability.

### Note:
`z-index` creates stacking contexts only if the element is positioned (`position` other than `static`) and, in some cases, if it has specific properties like `opacity` less than 1 or CSS transforms.

---

**Summary:**
```plaintext
z-index: <integer>;
```
- Determines stacking order
- Works with positioned elements
- Higher numbers overlay lower ones

Let me know if you'd like an example demonstrating stacking contexts or more advanced usage!

---
Master layering with `z-index` for perfect stacking orders in your layouts—see clear examples and pro tips!