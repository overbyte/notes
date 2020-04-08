

# Examples

Executed as part of find (see using-find note)

* -E use extended regex
* -i update in place (ie replace existing file - remove this to test a `sed`)
* `/\@automotive/!`
** using `!` makes this a negative lookbehind (equivalent) by creating a register
** surrounding with `/xx/` uses regex
* `s/(jlr-[^"]+)/@automotive\/\1/g`
** `(jlr-[^"]+)` create capture group from `jlr-everthing-not"`
** `s/xxx/g` makes this regex (with global flag)
** `[^"]+` greedy search for everything up to a `"`
** `\1` put everything in capture group 1 here

```
find ./ -type f -not -path '*/\.git/*' -exec sed -Ei '/\@automotive/!s/(jlr-[^"]+)/@automotive\/\1/g' {} \;
```

# Links

* 
