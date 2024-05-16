# Using find on the command line

## Examples

```bash
find ./src -name "*.tsx" -type
```

* find all `.tsx` files in the `/src` directory


```bash
find ./ -type f -not -path '*/\.git/*' -exec sed -Ei 's/epicgames/beijing/g' {} \;
```

This finds:

* type file
* but not in the path .git
* execute sed (see sed note) to replace epicgames with beijing

## Links

* https://bytefreaks.net/gnulinux/bash/how-to-execute-find-that-ignores-git-directories
