You can use the `diff` command with `--color=always` to compare two files and display the differences with color highlighting in the terminal.

Here’s how you do it:

```sh
diff --color=always file.js file2.js
```

### Explanation:
- `diff`: A Unix command-line tool used to compare files and show the differences.
- `--color=always`: Ensures that colorized output is always enabled.
- `file.js file2.js`: The two files you want to compare.

If your terminal doesn’t support color output, you might want to pipe the result through `less` with the `-R` flag to retain color formatting:

```sh
diff --color=always file.js file2.js | less -R
```

Let me know if you need additional refinements or alternative approaches!