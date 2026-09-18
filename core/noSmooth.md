# `noSmooth()`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
void noSmooth()
```

## Description

Disables anti-aliasing. Edges appear jagged/pixelated. Useful for pixel-art aesthetics, intentional retro looks, or squeezing out performance when smooth edges are not needed. Call in `setup()` before the first `draw()`.

## Parameters

_None._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `JAVA2D` | Disables `RenderingHints` anti-aliasing |
| `P2D` / `P3D` | Disables MSAA at framebuffer level; must be set in `setup()` |
| `FX2D` | Anti-aliasing cannot be fully disabled in JavaFX — call may have no effect |
| `PDF` / `SVG` | No effect — vector output is always crisp |

---

## Pitfalls

- Like `smooth()`, calling `noSmooth()` inside `draw()` in P2D/P3D triggers a full renderer reset — call it only in `setup()`.
- On `FX2D`, `noSmooth()` is effectively a no-op — JavaFX always renders with sub-pixel AA.

---

## Examples

```processing
// Pixel-art style sketch
void setup() {
  size(400, 400);
  noSmooth();
  noStroke();
}

void draw() {
  background(0);
  fill(0, 255, 100);
  // Crisp, aliased edges
  rect(mouseX - 10, mouseY - 10, 20, 20);
}
```

---

## Related Functions

- [`smooth()`](smooth.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
