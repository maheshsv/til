# Copy in Vim

### cut/copy and paste in visual mode, [here](http://vim.wikia.com/wiki/Copy,_cut_and_paste)

* `v`
* Move cursor to select content
* `d` to cut or `y` to copy
* `p` to paste

### copy to clipboard in Mac, [here](https://stackoverflow.com/questions/3961859/how-to-copy-to-clipboard-in-vim)

* `v`
* type `:w !pbcopy` or `:%w !pbcopy` for the whole file
* paste from clipboard `:r !pbpaste`

### copy the entire file: `ggyG`
