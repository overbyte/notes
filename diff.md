# Diff

There are several ways to run diffs in Bash

```
diff # standard diff
vimdiff # side-by-side diff in vim
```

## Sorting before diff

Using `sort` allows us to sort the lines to ensure that the diff takes all of
the content into account

```
diff <(sort file1) <(sort file2)
```
Source:
https://unix.stackexchange.com/questions/23303/diff-where-lines-are-mostly-the-same-but-out-of-order?newreg=bb4c53c3b14f44f18c189f1d8136af28
