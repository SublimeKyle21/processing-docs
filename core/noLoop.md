# `noLoop()`

> **Category:** Core — Lifecycle  
> **Status:** ✅ Complete

---

## Signature

```processing
void noLoop()
```

## Description

Stops `draw()` from being called repeatedly. After `noLoop()` is invoked, the sketch executes `draw()` one final time to completion, then halts the animation loop. The sketch window remains open and visible.

Calling `noLoop()` inside `setup()` is a common pattern for static or event-driven sketches — render once, then wait for user input.

## Parameters

_None._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Uniform behavior across renderers |

---

## Implementation Notes

- Sets an internal flag; the current `draw()` call (if any) runs to completion before the loop stops.
- Mouse and keyboard events still fire while the loop is stopped — only `draw()` is paused.
- `frameCount` stops incrementing after the loop stops.

---

## Pitfalls

- Event callbacks (`mousePressed()`, etc.) still fire after `noLoop()` — if they modify sketch state you expect `draw()` to reflect, call `redraw()` manually at the end of the handler.
- Calling `noLoop()` then never calling `loop()` or `redraw()` can leave the sketch in a permanently frozen state, confusing users.
- Don't confuse `noLoop()` with stopping the sketch entirely — use `exit()` for that.

---

## Examples

```processing
// Render once, then stop
void setup() {
  size(600, 400);
  noLoop();
}

void draw() {
  background(240);
  for (int i = 0; i < 200; i++) {
    stroke(random(255));
    line(random(width), random(height), random(width), random(height));
  }
}

// Re-render on click
void mousePressed() {
  redraw();
}
```

---

## Related Functions

- [`loop()`](loop.md)
- [`redraw()`](redraw.md)
- [`draw()`](draw.md)
- [`exit()`](exit.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
