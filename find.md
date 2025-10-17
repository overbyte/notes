# Using find on the command line

## Examples

```bash
find ./src -name "*.tsx" -type
```

- find all `.tsx` files in the `/src` directory

```bash
find ./ -type f -not -path '*/\.git/*' -exec sed -Ei 's/epicgames/beijing/g' {} \;
```

This finds:

- type file
- but not in the path .git
- execute sed (see sed note) to replace epicgames with beijing

```bash
find . -name 'node_modules' -type d -prune -exec rm -rf {} \;
```

This finds all `node_modules` folders (but not the contents) and deletes them

- `-prune` stops `find` descending into `node_modules` folders it finds

## Links

- https://bytefreaks.net/gnulinux/bash/how-to-execute-find-that-ignores-git-directories
