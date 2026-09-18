# `fullScreen()`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
void fullScreen()
void fullScreen(int display)
void fullScreen(String renderer)
void fullScreen(String renderer, int display)
void fullScreen(SPAN)
```

## Description

Opens the sketch as a fullscreen window, automatically setting `width` and `height` to the monitor's resolution. Like `size()`, it must be the **first statement in `setup()`**.

Pass a display number (1-based) to target a specific monitor on a multi-monitor setup. Pass `SPAN` (instead of a display number) to span all connected displays as a single canvas.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `display` | `int` | `1` | Monitor number (1 = primary) |
| `renderer` | `String` | `JAVA2D` | Same renderer options as `size()` |
| `SPAN` | constant | — | Span the sketch across all displays |

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `JAVA2D` | Borderless window at display resolution |
| `P2D` / `P3D` | Native fullscreen via LWJGL; may capture the display exclusively on some systems |
| `FX2D` | JavaFX fullscreen; press `Escape` to exit unless `keyPressed()` intercepts it |

---

## Implementation Notes

- `width` and `height` are set to the display's logical resolution after `fullScreen()`.
- On macOS with Retina displays, `width`/`height` are logical points — `pixelWidth`/`pixelHeight` are 2× larger.
- `SPAN` mode sets `width` to the combined width of all monitors and `height` to the tallest monitor.
- Pressing `Escape` in a fullscreen P2D/P3D sketch calls `exit()` by default — override `keyPressed()` to prevent this.

---

## Pitfalls

- On Linux with some window managers, `fullScreen()` may not remove the taskbar — use `surface.setAlwaysOnTop(true)` as a workaround.
- `SPAN` mode with monitors of different heights produces a canvas taller than some monitors — you must account for this in layout.
- Calling `fullScreen()` with a display index that doesn't exist falls back to the primary display without warning.
- In the PDE, fullscreen sketches take over the screen — press `Escape` or `Ctrl+W` to return to the IDE.

---

## Examples

```processing
// Fullscreen on primary display, default renderer
void setup() {
  fullScreen();
  background(0);
}

void draw() {
  fill(255, 10);
  ellipse(mouseX, mouseY, 80, 80);
}
```

```processing
// P3D fullscreen on second monitor
void setup() {
  fullScreen(P3D, 2);
  smooth(4);
}

void draw() {
  background(10);
  lights();
  translate(width / 2, height / 2);
  rotateY(frameCount * 0.01);
  sphere(200);
}
```

```processing
// Span across all monitors
void setup() {
  fullScreen(SPAN);
  background(0);
  textSize(40);
  fill(255);
  textAlign(CENTER, CENTER);
  text("Spanning " + width + " x " + height, width / 2, height / 2);
  noLoop();
}
```

---

## Related Functions

- [`size()`](size.md)
- [`width`](width.md)
- [`height`](height.md)
- [`displayWidth`](displayWidth.md)
- [`pixelDensity()`](pixelDensity.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
