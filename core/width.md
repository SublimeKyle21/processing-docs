# `width`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
int width
```

## Description

A built-in read-only variable containing the width of the sketch canvas in pixels, as set by `size()` or `fullScreen()`. Available after `size()` is called; equals `100` by default if `size()` has not been called yet.

Use `width` instead of hard-coding pixel values to make sketches resolution-independent and easy to resize.

## Parameters

_System variable — not a function._

## Returns

`int` — canvas width in pixels

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Always reflects the logical (CSS) pixel width, not the physical pixel width |
| P2D / P3D with `pixelDensity(2)` | Physical pixel width is `width * pixelDensity` — use `pixelWidth` for the physical dimension |

---

## Implementation Notes

- `width` is set during `size()` and does not change unless the renderer is re-initialized.
- On HiDPI displays with `pixelDensity(2)`, `width` still reports the logical size. Use `pixelWidth` for the actual backing-store width when accessing `pixels[]`.
- Resizing the window (via `surface.setResizable(true)`) does **not** update `width` automatically in Processing 3/4 — listen to `windowResized()` if needed.

---

## Pitfalls

- Accessing `width` before `size()` returns `100` (the default sketch size) — can cause layout bugs if read during field initialization.
- Confusing `width` (logical pixels) with `pixelWidth` (physical pixels) on retina displays causes off-by-2x errors in pixel-level operations.
- Do not reassign `width` — it is a `public int` field but overwriting it desynchronizes it from the actual renderer dimensions.

---

## Examples

```processing
void setup() {
  size(800, 400);
}

void draw() {
  background(30);
  // Always centered regardless of canvas size
  ellipse(width / 2, height / 2, 100, 100);

  // Responsive grid
  int cols = 8;
  float colW = width / float(cols);
  for (int i = 0; i < cols; i++) {
    line(i * colW, 0, i * colW, height);
  }
}
```

---

## Related Functions

- [`height`](height.md)
- [`size()`](size.md)
- [`pixelDensity()`](pixelDensity.md)
- [`displayWidth`](displayWidth.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
