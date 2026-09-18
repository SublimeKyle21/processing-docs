# `exit()`

> **Category:** Core — Lifecycle  
> **Status:** ✅ Complete

---

## Signature

```processing
void exit()
```

## Description

Gracefully terminates the sketch. `exit()` finishes the current `draw()` call, runs any registered `dispose()` or shutdown hooks, closes the renderer, and exits the JVM (when running as an application). It is the preferred way to quit a sketch programmatically.

Do not use `System.exit()` directly — it bypasses Processing's cleanup routines and can corrupt PDF/SVG output files and leave OpenGL contexts unreleased.

## Parameters

_None._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `default` (Java2D) | Disposes AWT window and exits JVM |
| `P2D` / `P3D` | Releases OpenGL context and VRAM before exit |
| `PDF` | Flushes and closes the PDF file — **critical**: skipping `exit()` can produce a corrupt/unreadable PDF |
| `SVG` | Same as PDF — must call `exit()` to finalize the SVG output |
| `FX2D` | Shuts down JavaFX platform cleanly |

---

## Implementation Notes

- Internally calls `finished = true` and schedules a `dispose()` call on the animation thread.
- When running inside the PDE (IDE), `exit()` stops the sketch but does not close the editor window.
- When running as an exported application, `exit()` terminates the JVM process entirely.
- A registered `dispose()` method (via `registerMethod("dispose", this)`) is called just before shutdown.

---

## Pitfalls

- Using `System.exit(0)` instead of `exit()` skips renderer cleanup — avoid it entirely in Processing sketches.
- Calling `exit()` inside `setup()` before `size()` can leave a blank window momentarily before the JVM stops.
- For PDF/SVG sketches that record output, forgetting `exit()` is the #1 cause of empty or truncated output files.
- In libraries that spawn threads, those threads may not be stopped by `exit()` — join/interrupt them explicitly in `dispose()`.

---

## Examples

```processing
// Quit after saving a frame
void setup() {
  size(800, 600);
  noLoop();
}

void draw() {
  background(30);
  fill(255);
  textSize(32);
  textAlign(CENTER, CENTER);
  text("Saving and quitting...", width / 2, height / 2);
  saveFrame("output-####.png");
  exit();
}
```

```processing
// Quit on key press
void draw() {
  background(80);
}

void keyPressed() {
  if (key == 'q' || key == ESC) {
    exit();
  }
}
```

---

## Related Functions

- [`setup()`](setup.md)
- [`draw()`](draw.md)
- [`noLoop()`](noLoop.md)
- [`registerMethod()`](registerMethod.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
