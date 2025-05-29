Yes, it is possible to set the `value` attribute for a `<select>` element even if its `innerHTML` is empty. The `value` attribute of a `<select>` element is typically set on its `<option>` elements. If you have a `<select>` element with no options, you can still set its `value` attribute programmatically using JavaScript.

Here’s an example:

```html
<select id="mySelect"></select>

<script>
    // Create an option element
    var option = document.createElement("option");
    option.value = "1"; // Set the value attribute
    option.text = "Option 1"; // Set the display text

    // Append the option to the select element
    document.getElementById("mySelect").appendChild(option);

    // Set the select's value
    document.getElementById("mySelect").value = "1"; // This will select "Option 1"
</script>
```

In this example, we create an option with a value of "1" and append it to the `<select>` element. After that, we set the value of the `<select>` to "1", which selects the newly added option. 

If you want to set the value of the `<select>` element without any options, it will not have any visible effect until you add options to it.