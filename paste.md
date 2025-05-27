To view the diff of two files (`file.js` and `file2.js`) with color highlighting in a terminal, you typically use `diff` with the `--color=always` option. The command looks like this:

```sh
diff --color=always file.js file2.js
```

### Additional options and best practices:

- **For readable, colorized output in the terminal:**

  ```sh
  diff --color=always file.js file2.js
  ```

- **If you want to compare files in a more readable, side-by-side format**, consider using `diff` with the `-y` option:

  ```sh
  diff -y --color=always file.js file2.js
  ```

- **Using `colordiff` for more semantic coloring:**

  You can install [`colordiff`](https://github.com/rrthomas/colordiff), a wrapper around `diff` that adds syntax highlighting. Use it as:

  ```sh
  colordiff file.js file2.js
  ```

  To do this, first install it:

  ```sh
  sudo apt-get install colordiff  # Debian/Ubuntu
  # or
  brew install colordiff      # MacOS with Homebrew
  ```

### Important tips:

- **Enabling color in your CLI**: Ensure your terminal supports color output.
- **Using `diff` with `less`**: To paginate long output with color, pipe it through `less -R`:

  ```sh
  diff --color=always file.js file2.js | less -R
  ```

---

### Summary

- To directly compare two files with color:

  ```sh
  diff --color=always file.js file2.js
  ```

- For side-by-side comparison:

  ```sh
  diff -y --color=always file.js file2.js
  ```

- For enhanced readability, consider `colordiff`.

---

**Note:** The `--color=always` option is supported in GNU `diff`. If you're using BSD `diff` (like on macOS), it may not support this option natively. In such cases, you can either install GNU `diff` (via coreutils) or use third-party tools as mentioned.

---

Let me know if you'd like help with scripts or integrating diff functionalities into your development workflow!