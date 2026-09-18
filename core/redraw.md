# `redraw()`

> **Category:** Core — Lifecycle  
> **Status:** ✅ Complete

---

## Signature

```processing
void redraw()
```

## Description

Executes `draw()` exactly once. Only meaningful when the loop has been stopped with `noLoop()`. `redraw()` is the standard way to trigger a single repaint in event-driven or on-demand sketches.

## Parameters

_None._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Uniform — triggers one `draw()` cycle |

---

## Implementation Notes

- If the loop is running (`loop()` state), calling `redraw()` has no additional effect — `draw()` is already being called continuously.
- Safe to call from event handlers, `thread()` callbacks, and Swing listeners.
- `frameCount` increments by 1 per `redraw()` call.

---

## Pitfalls

- Calling `redraw()` from within `draw()` itself creates an infinite synchronous call stack — never do this.
- Multiple rapid `redraw()` calls from an event handler do not queue multiple frames; they collapse into however many the animation thread can service.

---

## Examples

```processing
int col = 0;

void setup() {
  size(400, 400);
  noLoop();
  background(col);
}

void draw() {
  background(col);
}

void keyPressed() {
  col = (col + 20) % 256;
  redraw();   // repaint with new background color
}
```

---

## Related Functions

- [`noLoop()`](noLoop.md)
- [`loop()`](loop.md)
- [`draw()`](draw.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
