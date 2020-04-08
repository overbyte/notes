
# Examples

This finds:

* type file
* but not in the path .git
* execute sed (see sed note) to replace epicgames with beijing

```
find ./ -type f -not -path '*/\.git/*' -exec sed -Ei 's/epicgames/beijing/g' {} \;
```

# Links

* https://bytefreaks.net/gnulinux/bash/how-to-execute-find-that-ignores-git-directories
