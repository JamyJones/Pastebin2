In Bootstrap 5, the `z-index` property is used to control the stacking order of elements on the page. It determines which elements appear on top of others when they overlap. The `z-index` value can be set using utility classes provided by Bootstrap.

### Bootstrap 5 `z-index` Utility Classes

Bootstrap 5 includes several predefined utility classes for setting `z-index` values:

- `.z-index-0`: Sets `z-index` to `0`
- `.z-index-1`: Sets `z-index` to `100`
- `.z-index-2`: Sets `z-index` to `200`
- `.z-index-3`: Sets `z-index` to `300`
- `.z-index-4`: Sets `z-index` to `400`
- `.z-index-5`: Sets `z-index` to `500`

### Usage Example

You can apply these classes to any element to control its stacking order. For example:

```html
<div class="position-relative">
  <div class="position-absolute z-index-1">This is behind</div>
  <div class="position-absolute z-index-2">This is in front</div>
</div>
```

In this example, the second `div` with `z-index-2` will appear in front of the first `div` with `z-index-1` due to its higher `z-index` value.

### Important Notes

- The `z-index` property only works on positioned elements (i.e., elements with a position value of `relative`, `absolute`, `fixed`, or `sticky`).
- The default stacking context is determined by the `z-index` of the parent elements, so ensure that the parent elements are also positioned if you want to control the stacking order effectively.