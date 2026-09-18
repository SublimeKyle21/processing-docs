# `pixelDensity()`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
void pixelDensity(int density)
```

## Description

Sets the pixel density of the sketch — critical for sharp rendering on HiDPI (Retina) displays. A density of `2` doubles the number of physical pixels used for the canvas while keeping `width` and `height` at their logical values. Use `displayDensity()` to automatically match the display's native pixel ratio.

**Must be called immediately after `size()` in `setup()`.**

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `density` | `int` | `1` | Pixel density multiplier: `1` (standard) or `2` (HiDPI/Retina) |

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `JAVA2D` | Scales the AWT canvas backing store |
| `P2D` / `P3D` | Scales the OpenGL framebuffer; `pixelWidth` = `width * density` |
| `FX2D` | JavaFX manages HiDPI natively; `pixelDensity()` may be redundant |
| `PDF` / `SVG` | No effect — vector renderers are resolution-independent |

---

## Implementation Notes

- After calling `pixelDensity(2)`, `pixelWidth = width * 2` and `pixelHeight = height * 2`.
- When accessing `pixels[]`, always use `pixelWidth` and `pixelHeight` for array dimensions, not `width` and `height`.
- `displayDensity()` returns the OS-reported device pixel ratio (1.0, 1.5, 2.0, etc.) — passing it to `pixelDensity()` is the standard idiom.
- Setting density > 2 is valid syntactically but unsupported on current hardware and has no additional effect.

---

## Pitfalls

- Forgetting `pixelDensity(displayDensity())` on a Retina Mac makes the sketch render at 1× and appear blurry — the most common HiDPI pitfall.
- Using `width` instead of `pixelWidth` when iterating `pixels[]` on a 2× display accesses only a quarter of the actual pixel buffer — causes visual corruption.
- `pixelDensity()` must precede `smooth()` in `setup()` — some renderer combinations behave incorrectly if the order is reversed.
- Calling `pixelDensity()` in `draw()` has no effect — it's a setup-time-only setting.

---

## Examples

```processing
void setup() {
  size(800, 600, P2D);
  pixelDensity(displayDensity());   // auto-match display DPI
  smooth(4);
  background(0);
}

void draw() {
  // pixelWidth / pixelHeight are the true framebuffer dimensions
  fill(255);
  textSize(14);
  text("Logical: " + width + "x" + height, 10, 20);
  text("Physical: " + pixelWidth + "x" + pixelHeight, 10, 40);
}
```

```processing
// Correct pixel[] iteration on HiDPI
void setup() {
  size(400, 400);
  pixelDensity(2);
  loadPixels();
  for (int y = 0; y < pixelHeight; y++) {
    for (int x = 0; x < pixelWidth; x++) {
      pixels[y * pixelWidth + x] = color(x % 255, y % 255, 128);
    }
  }
  updatePixels();
  noLoop();
}
```

---

## Related Functions

- [`displayDensity()`](displayDensity.md)
- [`size()`](size.md)
- [`fullScreen()`](fullScreen.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
