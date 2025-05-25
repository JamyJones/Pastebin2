To select all `<button>`, `<select>`, and `<input>` elements within a `<div>` element with the ID `foo`, you can use a CSS descendant selector combined with a comma-separated list of element types.

### CSS Selector:
```css
#foo button,
#foo select,
#foo input {
  /* Your styles here */
}
```

### Explanation:
- `#foo` targets the element with `id="foo"`.
- Each comma-separated selector (`button`, `select`, `input`) targets those specific elements that are descendants of `#foo`.
- Together, this ruleset applies styles to all `<button>`, `<select>`, and `<input>` elements within the `<div id="foo">`.

### Example:
```css
#foo button,
#foo select,
#foo input {
  border: 2px solid #007BFF;
  padding: 8px;
  border-radius: 4px;
}
```

This will style all matching elements within the specified `<div>`.

---

### Summary:
- Use `#foo` as the parent selector.
- List all target elements separated by commas for group styling.
- This is a clean, efficient way to target multiple element types within a specific container.