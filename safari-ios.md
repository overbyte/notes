# Handling Safari on iOS for PWA

## App Level Fixes

disable doubleclick to fix zoom and scroll issues on doubleclick

```
document.addEventListener('dblclick', (e) => {
  e.preventDefault();
});
```

#### disable contextmenu

```
document.addEventListener('contextmenu', (e) => {
  e.preventDefault();
});
```

I also found that `oncontextmenu` may be necessary to catch all instances for no
reason I can really tell.

This will eliminate context menus as well as some press-to-hold items for
anchors and images (but not all)

```
  <main class="app view" oncontextmenu="return false">
    <router-view></router-view>
  </main>
```

#### disable touch-action in CSS

```
.app {
  touch-action: none;
}
```

#### Basic CSS overrides

- `-webkit-touch-callout: none` will disable the context menus
- `user-select: none` will fix a number of issues but may cause issues with
  `<input>` or `<textarea>`. Using `:not(input, textarea) {}` may solve this
- `user-drag: none` is a deprecated CSS that should work the same as setting
  `draggable="false"` on the element but it's more convenient to do this
  across the app in CSS

```
*,
*:before,
*:after {
  box-sizing: border-box;
  -webkit-touch-callout: none;
  user-select: none;
}

a,
img {
  -webkit-user-drag: none;
  -khtml-user-drag: none;
  -moz-user-drag: none;
  -o-user-drag: none;
  user-drag: none;
}
```

## Complete Safari CSS Reference

https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-_webkit_touch_callout
