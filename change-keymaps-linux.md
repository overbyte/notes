# Updating keymaps in X11 (Linux)

## AKA turning off the flippin' Caps Lock key - could also be used to make that
weird symbol at the top left of an Apple keyboard into a hard escape key
amiright?

Create a file at `touch ~/.Xmodmap` with the following contents:

```
clear lock
keycode  66 = Control_L NoSymbol Control_L NoSymbol Control_L
add lock = Caps_Lock
```

Ubuntu should pick this up on restart but if not, add a file `~/.xinitrc`

```
if [ -s ~/.Xmodmap ]; then
    xmodmap ~/.Xmodmap
fi
```

## Links

* http://xahlee.info/linux/linux_xmodmap_tutorial.html
