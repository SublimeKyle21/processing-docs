# `height`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
int height
```

## Description

A built-in read-only variable containing the height of the sketch canvas in pixels, as set by `size()` or `fullScreen()`. Mirrors `width` in every respect — see `width` for full details.

## Parameters

_System variable — not a function._

## Returns

`int` — canvas height in pixels

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Logical pixel height — see `pixelHeight` for the physical height on HiDPI displays |

---

## Pitfalls

- Same as [`width`](width.md): do not read before `size()`, do not reassign, and distinguish from `pixelHeight` on retina displays.

---

## Examples

```processing
void setup() {
  size(600, 400);
  background(20);
  // Vertical center line
  line(0, height / 2, width, height / 2);
}
```

---

## Related Functions

- [`width`](width.md)
- [`size()`](size.md)
- [`pixelDensity()`](pixelDensity.md)
- [`displayHeight`](displayHeight.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
