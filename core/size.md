# `size()`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
void size(int width, int height)
void size(int width, int height, String renderer)
void size(int width, int height, String renderer, String path)
```

## Description

Sets the width and height of the sketch canvas and selects the rendering engine. **Must be the first statement in `setup()`** — placing it anywhere else causes a warning and unpredictable behavior. After `size()` is called, the `width` and `height` system variables are set.

The optional `renderer` argument selects the graphics backend. The optional `path` argument is required for file-output renderers (`PDF`, `SVG`).

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `width` | `int` | `100` | Canvas width in pixels |
| `height` | `int` | `100` | Canvas height in pixels |
| `renderer` | `String` | `JAVA2D` | Renderer: `P2D`, `P3D`, `PDF`, `SVG`, `FX2D` |
| `path` | `String` | — | Output file path; required for `PDF` and `SVG` renderers |

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `JAVA2D` (default) | Software-rendered, best compatibility, no GPU requirement |
| `P2D` | OpenGL 2D; hardware-accelerated, supports shaders, requires GPU |
| `P3D` | OpenGL 3D; full 3D pipeline, lighting, shaders |
| `PDF` | Renders directly to a PDF file; no interactive window by default |
| `SVG` | Renders directly to an SVG file; no interactive window |
| `FX2D` | JavaFX backend; smoother font rendering, requires JavaFX runtime |

---

## Implementation Notes

- Processing uses Java reflection to detect `size()` at parse time — it must be a literal call at the top of `setup()`, not wrapped in a conditional or helper function.
- Maximum canvas size is limited by available RAM (Java2D) or VRAM (P2D/P3D). Very large canvases (>4096×4096) may silently fail on some GPUs.
- For P2D/P3D, OpenGL textures are limited by `GL_MAX_TEXTURE_SIZE` on the device (typically 8192–16384 px per side).
- `size()` cannot be called more than once per sketch without re-initializing the renderer — use `surface.setSize()` for dynamic resizing.

---

## Pitfalls

- Calling `size()` inside `draw()` reinitializes the renderer every frame — a catastrophic performance bug.
- Wrapping `size()` in a method call (e.g., `setupCanvas()` that calls `size()`) breaks Processing's static parser — `size()` must appear literally in `setup()`.
- Sizes larger than `displayWidth` × `displayHeight` create windows that extend off-screen — use `fullScreen()` instead.
- Forgetting `path` with `PDF`/`SVG` causes a runtime error: `size(400, 400, PDF)` → must be `size(400, 400, PDF, "output.pdf")`.

---

## Examples

```processing
// Default Java2D renderer
void setup() {
  size(800, 600);
}
```

```processing
// OpenGL 2D with smooth anti-aliasing
void setup() {
  size(1280, 720, P2D);
  smooth(8);
}
```

```processing
// Save a PDF
import processing.pdf.*;

void setup() {
  size(595, 842, PDF, "poster.pdf");  // A4 at 72 dpi
  background(255);
  fill(30);
  textSize(48);
  text("Hello PDF", 80, 400);
  exit();  // finalize and close the PDF
}
```

```processing
// 3D scene
void setup() {
  size(800, 600, P3D);
}

void draw() {
  background(0);
  lights();
  translate(width/2, height/2, 0);
  rotateY(frameCount * 0.02);
  box(150);
}
```

---

## Related Functions

- [`fullScreen()`](fullScreen.md)
- [`width`](width.md)
- [`height`](height.md)
- [`pixelDensity()`](pixelDensity.md)
- [`smooth()`](smooth.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
