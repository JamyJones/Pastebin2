In CSS, `z-index` is a property that controls the stacking order of overlapping elements. Elements with a higher `z-index` are displayed in front of those with a lower `z-index`.

### `z-index` in Bootstrap 5

Bootstrap 5, like many CSS frameworks, uses the `z-index` property to manage the layering of components such as modals, dropdowns, tooltips, and other positioned elements to ensure they appear above or below each other correctly.

#### Default `z-index` Values in Bootstrap 5

Bootstrap 5 defines specific `z-index` levels for its components within its CSS, mainly through the `z-index` utility classes and component-specific styles. These are set using CSS custom properties or explicit rules in the framework:

| Class or Component      | `z-index` value       | Usage                                          |
|-------------------------|-----------------------|------------------------------------------------|
| `.modal`               | 1050                  | Modal dialog boxes                              |
| `.dropdown-menu`       | 1000                  | Dropdown menus                                |
| `.tooltip`             | 1070                  | Tooltips                                       |
| Navbar (sticky)        | 1020                  | Sticky navigation bars                         |
| Alerts, Toasts        | Varies (1030+ )        | Alerts, toasts for notifications              |

#### Example of `z-index` in Bootstrap 5

```html
<div class="popup" style="position: absolute; z-index: 1050;">
  Modal-like element
</div>
```

In Bootstrap 5, you would rarely need to set `z-index` manually for built-in components because Bootstrap handles this internally. However, if you are creating custom components that overlap, you may want to manage `z-index` for proper stacking.

### Custom Utility Classes with `z-index`

Bootstrap 5 provides utility classes to easily manage `z-index`. For example:

```html
<div class="z-1">z-index: 1</div>
<div class="z-10">z-index: 10</div>
<div class="z-auto">z-index: auto</div>
```

These classes correspond to predefined `z-index` values in Bootstrap’s CSS.

### Summary

- `z-index` controls the stacking order of elements.
- Bootstrap 5 defines specific `z-index` values for its components.
- Use utility classes like `.z-1`, `.z-10`, `.z-auto` for quick management.
- When creating your custom layered components, adjust `z-index` to ensure correct overlaying.

---

**Example Usage in a Custom Overlay:**

```html
<div class="overlay z-10" style="position: fixed; top:0; left:0; width:100%; height:100%; background: rgba(0,0,0,0.5);"></div>
```

This overlay will appear above elements with lower `z-index`.

---

Would you like specific code examples for creating overlapping components or managing stacking order in Bootstrap 5?