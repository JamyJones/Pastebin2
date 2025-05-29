To improve the performance of Vim when opening large text files, you can consider removing or modifying certain settings in your `.vimrc` file. Here are some suggestions:

1. **Disable Syntax Highlighting**: Syntax highlighting can slow down Vim with large files. You can disable it for large files or entirely if you don't need it.
   ```vim
   syntax off
   ```

2. **Disable Line Numbers**: Line numbers can also slow down performance. You can disable them or set them to be shown only in certain file types.
   ```vim
   set nonumber
   ```

3. **Disable Search Highlighting**: If you don't need search highlighting, you can disable it.
   ```vim
   set nohlsearch
   ```

4. **Disable Auto Indentation**: Auto indentation can slow down performance with large files.
   ```vim
   set paste
   ```

5. **Reduce Command Height**: If you don't need a large command height, you can set it to a smaller value.
   ```vim
   set cmdheight=0
   ```

6. **Disable Wildmenu**: The wildmenu can slow down performance, especially with large files.
   ```vim
   set nowildmenu
   ```

7. **Disable Folding**: If you have folding enabled, it can slow down performance with large files.
   ```vim
   set nofoldenable
   ```

8. **Lazy Redraw**: You already have `set lazyredraw`, which is good for performance. Ensure it remains.

9. **Avoid Plugins**: If you have any plugins that are not essential for coding, consider disabling them when working with large files.

Here’s a modified section of your `.vimrc` with the suggested changes:

```vim
" Disable syntax highlighting for large files
syntax off

" Disable line numbers
set nonumber

" Disable search highlighting
set nohlsearch

" Disable auto indentation
set paste

" Reduce command height
set cmdheight=0

" Disable wildmenu
set nowildmenu

" Disable folding
set nofoldenable
```

You can add these lines to your `.vimrc` file. If you want to keep some features but improve performance, consider using conditional statements to disable them only for large files. For example:

```vim
if line('$') > 1000
    syntax off
    set nonumber
    set nohlsearch
    set paste
endif
```

This way, you can maintain your preferred settings for smaller files while optimizing for larger ones.