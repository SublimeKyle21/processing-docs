# `draw()`

> **Category:** Core — Lifecycle  
> **Status:** ✅ Complete

---

## Signature

```processing
void draw()
```

## Description

Called repeatedly at the rate set by `frameRate()` (default 60 fps). Everything that changes frame-to-frame — motion, user interaction, simulations — belongs inside `draw()`. Processing calls `draw()` automatically on the animation thread after `setup()` completes.

If `draw()` is not defined, the sketch runs in **static mode**: `setup()` (or top-level code) executes once, the canvas is displayed, and the program halts. Most interactive sketches define both `setup()` and `draw()`.

## Parameters

_None — `draw()` takes no parameters._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `default` (Java2D) | Redraws to a buffered image each frame; `background()` is cheap |
| `P2D` | OpenGL double-buffered; not calling `background()` accumulates draw calls on the GPU — can produce intended trail effects but consumes VRAM faster |
| `P3D` | Same as P2D; depth buffer is cleared each frame only when `background()` is called |
| `PDF` / `SVG` | Each `draw()` call appends a page/frame to the output file when recording |
| `FX2D` | Runs on JavaFX application thread; long frames block UI events |

---

## Implementation Notes

- The loop is driven by `java.lang.Thread.sleep()` timing in Java2D and by OpenGL `swapBuffers()` sync in P2D/P3D.
- `frameCount` increments by 1 each time `draw()` completes.
- Calling `noLoop()` inside `draw()` stops the loop after the current frame finishes.
- `draw()` is **not** thread-safe — modifying shared data from other threads without synchronization causes race conditions.
- Processing does not guarantee exactly 60 fps — if `draw()` takes longer than one frame period, frames are dropped rather than queued.

---

## Pitfalls

- Forgetting `background()` at the start of `draw()` leaves previous frames visible — intentional for trails, a bug for most other cases.
- Expensive operations (file I/O, network, heavy computation) inside `draw()` stall the frame loop. Move them to `thread()` or a `Thread` subclass.
- Calling `size()` or `fullScreen()` inside `draw()` resets the renderer each frame — never do this.
- Global state modified inside an event handler (`mousePressed()`, `keyPressed()`, etc.) is accessed from the event thread, not the draw thread. Use `volatile` or `synchronized` for shared variables when this matters.
- `draw()` is called on the animation thread; Swing/AWT components must be updated on the EDT — use `javax.swing.SwingUtilities.invokeLater()`.

---

## Examples

```processing
float angle = 0;

void setup() {
  size(600, 600);
  background(20);
}

void draw() {
  background(20);                        // clear each frame
  translate(width / 2, height / 2);
  rotate(angle);
  rect(-60, -60, 120, 120);
  angle += 0.02;
}
```

```processing
// Intentional no-background trail effect
void setup() {
  size(800, 400);
  background(0);
  stroke(255, 30);
  noFill();
}

void draw() {
  // no background() call — draws accumulate
  ellipse(mouseX, mouseY, 60, 60);
}
```

---

## Related Functions

- [`setup()`](setup.md)
- [`loop()`](loop.md)
- [`noLoop()`](noLoop.md)
- [`redraw()`](redraw.md)
- [`frameRate()`](frameRate.md)
- [`frameCount`](frameCount.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
