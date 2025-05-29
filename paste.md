To improve the performance of Vim when opening large text files, you can consider removing or modifying certain settings in your `.vimrc` file. Here are some suggestions on what to remove or change:

1. **Remove or Comment Out Unused Plugins**: If you are not using certain plugins, consider commenting them out or removing them entirely. For example, if you are not using NERDTree or airline, you can comment out their related lines.

2. **Disable Syntax Highlighting**: Syntax highlighting can slow down Vim with large files. You can disable it for large files by adding the following line:
   ```vim
   syntax off
   ```

3. **Disable Line Wrapping**: If you don't need line wrapping, you can disable it:
   ```vim
   set nowrap
   ```

4. **Reduce Command Height**: You can set the command height to a lower value:
   ```vim
   set cmdheight=0
   ```

5. **Disable Search Highlighting**: If you don't need search highlighting, you can disable it:
   ```vim
   set nohlsearch
   ```

6. **Disable Auto Indentation**: If you don't need auto-indentation for large files, you can disable it:
   ```vim
   set paste
   ```

7. **Remove or Comment Out the Following Settings**: These settings can also contribute to slowness:
   ```vim
   set hlsearch
   set incsearch
   set showmatch
   set foldcolumn=1
   ```

8. **Lazy Redraw**: Ensure that `set lazyredraw` is enabled, as it can help with performance when executing macros.

9. **Remove or Comment Out the Following Autocommands**: Autocommands can slow down file opening:
   ```vim
   au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
   ```

10. **Disable Unused Filetype Plugins**: If you are not using certain file types, you can disable their plugins.

After making these changes, your `.vimrc` file should be more optimized for handling large files. Remember to restart Vim after modifying the configuration for the changes to take effect.