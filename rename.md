# Using rename on the command line

## Examples

for everything that includes the phrase `epicgames-2019`:

* replace `epicgames-2019` with `beijing-2020`

```
rename 's/epicgames-2019/beijing-2020/' *epicgames-2019*
```

for every file in the current directory:

* replace the first instance of a lowercase letter with an uppercase version of
  itself

```
rename 's/([a-z])/\U$1/' ./*
```

Changing case with transliteration of characters using `y/`

```
rename 'y/A-Z/a-z/' ./*
```

* source: https://stackoverflow.com/a/45641840
* description of `y/`: https://www.gnu.org/software/sed/manual/sed.html#Other-Commands

## Links

* https://www.howtogeek.com/423214/how-to-use-the-rename-command-on-linux/ 
* https://www.cyberciti.biz/tips/renaming-multiple-files-at-a-shell-prompt.html
