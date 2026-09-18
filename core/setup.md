# `setup()`

> **Category:** Core — Lifecycle  
> **Status:** ✅ Complete

---

## Signature

```processing
void setup()
```

## Description

Called once when the sketch starts. Use `setup()` to initialize state: set the canvas size, load assets, configure rendering options, and set initial variable values. Processing guarantees that `setup()` runs exactly once before any call to `draw()`.

The order of operations inside `setup()` matters. `size()` (or `fullScreen()`) **must be the first statement** — placing it anywhere else produces unpredictable behavior in some renderers. Asset loading (`loadImage()`, `loadFont()`, `loadTable()`, etc.) is safe here and happens synchronously.

## Parameters

_None — `setup()` takes no parameters._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `default` (Java2D) | Standard; `size()` must be first line |
| `P2D` | OpenGL context is created during `size()`; loading textures before `size()` will fail |
| `P3D` | Same as P2D |
| `PDF` | Output file must be specified in `size()` call |
| `SVG` | Output file must be specified in `size()` call |
| `FX2D` | JavaFX window created during `size()`; same constraint as P2D/P3D |

---

## Implementation Notes

- Processing uses reflection to detect whether the sketch defines `setup()`. If absent, the sketch is treated as static mode (no `draw()` loop either).
- In **static mode** (no `setup()`/`draw()`), all top-level statements execute once in order.
- `frameCount` is `0` during `setup()` and becomes `1` after the first `draw()` call.
- Global variables declared outside `setup()` and `draw()` are initialized before `setup()` runs.
- `setup()` runs on the main Processing/AWT event thread, not a separate thread.

---

## Pitfalls

- Calling `size()` anywhere other than the first line of `setup()` causes a warning in Processing 3+ and breaks layout in P2D/P3D.
- Loading large assets without a loading screen blocks the window from appearing — consider `thread()` for heavy async loads after `size()`.
- Putting animation logic in `setup()` instead of `draw()` runs it only once — a common beginner mistake.
- In Processing 4, the sketch window may briefly appear before `setup()` finishes on high-DPI displays; use `pixelDensity(displayDensity())` immediately after `size()` to avoid a resize flash.

---

## Examples

```processing
// Minimal sketch
void setup() {
  size(800, 600);
  background(30);
  noStroke();
  fill(255, 100, 50);
}

void draw() {
  ellipse(mouseX, mouseY, 40, 40);
}
```

```processing
// Setup with asset loading
PImage img;
PFont  font;

void setup() {
  size(640, 480, P2D);
  pixelDensity(displayDensity()); // retina / HiDPI support
  smooth(8);

  img  = loadImage("background.png");
  font = loadFont("Roboto-24.vlw");
  textFont(font);

  frameRate(60);
  background(0);
}
```

---

## Related Functions

- [`draw()`](draw.md)
- [`size()`](size.md)
- [`fullScreen()`](fullScreen.md)
- [`loop()`](loop.md) / [`noLoop()`](noLoop.md)
- [`frameRate()`](frameRate.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
