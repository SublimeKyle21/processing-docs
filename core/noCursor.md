# `noCursor()`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
void noCursor()
```

## Description

Hides the mouse cursor within the sketch window. The cursor disappears as soon as it enters the canvas area and reappears when it leaves. Commonly used in fullscreen installations, games, or when drawing a custom cursor with `image()` or `ellipse()` at `mouseX, mouseY`.

## Parameters

_None._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Uniform — hides the OS cursor over the canvas |

---

## Pitfalls

- The OS cursor reappears as soon as it leaves the sketch window — expected behavior but can look odd on partial-screen sketches.
- If you hide the cursor and draw a custom one, don't forget to call `noCursor()` every frame or at least once in `setup()` — moving the window sometimes restores the cursor on some platforms.
- In kiosk/fullscreen mode, users cannot move the cursor off the canvas, so `noCursor()` makes the cursor permanently invisible — ensure the sketch provides enough visual feedback for mouse position.

---

## Examples

```processing
void setup() {
  size(600, 400, P2D);
  noCursor();
}

void draw() {
  background(20);
  // Draw custom cursor
  fill(255, 200, 0);
  noStroke();
  ellipse(mouseX, mouseY, 20, 20);
  fill(255, 0, 0);
  ellipse(mouseX, mouseY, 6, 6);
}
```

---

## Related Functions

- [`cursor()`](cursor.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
