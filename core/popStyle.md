# `popStyle()`

> **Category:** Core — Style Stack  
> **Status:** ✅ Complete

---

## Signature

```processing
void popStyle()
```

## Description

Restores the style settings previously saved with `pushStyle()`. Must be balanced with a preceding `pushStyle()` call. Equivalent to the style-restore half of `pop()`.

## Parameters

_None._

## Returns

`void`

---

## Examples

```processing
void draw() {
  background(30);
  stroke(255);
  strokeWeight(1);

  pushStyle();
    stroke(255, 0, 0);
    strokeWeight(4);
    line(0, height/2, width, height/2);
  popStyle();

  // Stroke is back to white, weight 1
  line(0, height/3, width, height/3);
}
```

---

## Related Functions

- [`pushStyle()`](pushStyle.md)
- [`push()`](push.md)
- [`pop()`](pop.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
