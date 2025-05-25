You asked how to select all elements within a div element whose id is foo using CSS.

To achieve this, use the descendant selector. Here’s the syntax:

```css
#foo * {
  /* CSS properties here */
}
```

This selector targets all elements that are descendants of the element with id="foo". For example:

```css
#foo * {
  color: blue;
}
```

This will set the text color to blue for all elements inside the div with id="foo".