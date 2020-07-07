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

## Links

* https://www.howtogeek.com/423214/how-to-use-the-rename-command-on-linux/ 
