# `smooth()`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
void smooth()
void smooth(int level)
```

## Description

Enables anti-aliasing for all drawing operations. `smooth()` with no argument uses the default level (typically 2× MSAA in P2D/P3D, or system default in Java2D). Pass a `level` of `2`, `4`, or `8` to request multi-sample anti-aliasing (MSAA) — higher values produce smoother edges at the cost of GPU memory and fill rate.

Must be called in `setup()` for consistent results. Calling it inside `draw()` works in Java2D but causes a renderer reset each frame in P2D/P3D (severe performance impact).

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `level` | `int` | `2` | MSAA sample count: `2`, `4`, or `8` |

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `JAVA2D` | Uses Java2D `RenderingHints.VALUE_ANTIALIAS_ON`; `level` is ignored |
| `P2D` | Hardware MSAA; `level` must be `2`, `4`, or `8` — other values are clamped |
| `P3D` | Same as P2D; high MSAA on large framebuffers significantly impacts fill rate |
| `FX2D` | Anti-aliasing is always on; `level` is ignored |
| `PDF` / `SVG` | Vector output — always perfectly sharp; `smooth()` has no effect |

---

## Implementation Notes

- MSAA (multi-sample anti-aliasing) in P2D/P3D is set at framebuffer creation time — you cannot change it mid-sketch without re-creating the renderer.
- In Java2D, anti-aliasing is applied per-draw-call so it can technically be toggled per frame, but the visual difference is minor.
- `noSmooth()` disables anti-aliasing entirely, which can be useful for pixel-art sketches or performance-critical paths.

---

## Pitfalls

- Calling `smooth(8)` in Java2D silently ignores the argument — Java2D doesn't support MSAA levels.
- In P2D/P3D, calling `smooth()` inside `draw()` triggers a full OpenGL context reset — frame rate collapses to near zero. Always call it in `setup()`.
- Some GPUs cap MSAA at 4× even when 8× is requested — Processing accepts the GPU's actual maximum without throwing an error.
- `smooth()` does **not** affect `loadPixels()` / `updatePixels()` pixel manipulation — those work at the raw pixel level.

---

## Examples

```processing
void setup() {
  size(600, 400, P2D);
  smooth(8);   // 8x MSAA — smooth edges
}

void draw() {
  background(30);
  stroke(255);
  strokeWeight(1.5);
  for (int i = 0; i < 20; i++) {
    float angle = TWO_PI / 20 * i;
    line(width/2, height/2,
         width/2 + cos(angle) * 150,
         height/2 + sin(angle) * 150);
  }
}
```

---

## Related Functions

- [`noSmooth()`](noSmooth.md)
- [`size()`](size.md)
- [`strokeWeight()`](../shapes/attributes/strokeWeight.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
