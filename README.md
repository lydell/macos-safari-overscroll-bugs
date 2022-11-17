# macOS Safari overscroll color surprises

“Overscroll” means the rubber banding effect when you scroll up or down past the edges of the document.

[Live demo](https://lydell.github.io/macos-safari-overscroll-bugs/)

Keywords: macOS, Safari, meta, theme-color, overscroll, rubber banding, color, background-image, linear-gradient, opposite

## Explanation

If first believed I had found buggy behavior in Safari, and reported it: https://bugs.webkit.org/show_bug.cgi?id=247231

Turns it this is expected behavior! But it’s unintuitive and undocumented.

Here’s how I understand Safari’s rules for the overscroll color (in pseudo-code):

```
if background-image != none && (background-repeat == repeat || background-repeat == repeat-y) then
    use the page background
else if meta theme-color then
    use theme color
else
    use page background
```

Example:

1. `html { background-color: blue; }` results in blue overscroll.
2. Add `<meta name="theme-color" content="magenta" />` and you get magenta overscroll.
3. Add `html { background-image: linear-gradient(transparent, transparent); }` and you get _blue_ overscroll again!
4. Add `html { background-repeat: no-repeat; }` and you get magenta overscroll.
