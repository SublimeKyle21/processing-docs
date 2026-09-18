# `loop()`

> **Category:** Core — Lifecycle  
> **Status:** ✅ Complete

---

## Signature

```processing
void loop()
```

## Description

Resumes continuous execution of `draw()` after it has been stopped by `noLoop()`. If `draw()` is already running, calling `loop()` has no effect.

`loop()` is commonly called inside event handlers (`mousePressed()`, `keyPressed()`) to restart animation in response to user input.

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

- Internally sets a boolean flag that the animation thread checks at the end of each `draw()` cycle.
- Calling `loop()` does not immediately trigger a new `draw()` call — it re-enables the loop so the next scheduled frame proceeds.
- Safe to call from event handlers and `thread()` callbacks.

---

## Pitfalls

- Calling `loop()` before `setup()` finishes has no meaningful effect — the loop hasn't started yet.
- If `noLoop()` was called and no user interaction triggers `loop()` again, the sketch becomes permanently static (until `redraw()` is called manually).

---

## Examples

```processing
boolean running = false;

void setup() {
  size(400, 400);
  noLoop();   // start paused
}

void draw() {
  background(50);
  ellipse(frameCount % width, height / 2, 40, 40);
}

void mousePressed() {
  if (running) {
    noLoop();
  } else {
    loop();
  }
  running = !running;
}
```

---

## Related Functions

- [`noLoop()`](noLoop.md)
- [`redraw()`](redraw.md)
- [`draw()`](draw.md)
- [`frameRate()`](frameRate.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
