# Using vim

Some general notes that might be useful later

## changing case

```
 ~    : Changes the case of current character
 guu  : Change current line from upper to lower.
 gUU  : Change current LINE from lower to upper.
 guw  : Change to end of current WORD from upper to lower.
 guaw : Change all of current WORD to lower.
 gUw  : Change to end of current WORD from lower to upper.
 gUaw : Change all of current WORD to upper.
 g~~  : Invert case to entire line
 g~w  : Invert case to current WORD
 guG : Change to lowercase until the end of document.
```

source: https://stackoverflow.com/a/2966034/617603

## using autocomplete in vim-go

vim-go includes an autocomplete function ([doc](https://github.com/fatih/vim-go/blob/master/doc/vim-go.txt))

```
<C-x><C-o>
```
