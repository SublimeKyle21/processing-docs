# `frameCount`

> **Category:** Core — Lifecycle  
> **Status:** ✅ Complete

---

## Signature

```processing
int frameCount
```

## Description

A built-in read-only variable that holds the number of frames rendered since the sketch started. `frameCount` is `0` during `setup()`, becomes `1` after the first `draw()` call completes, and increments by 1 each frame thereafter. It is never reset during a sketch session.

## Parameters

_System variable — not a function; takes no parameters._

## Returns

`int` — current frame count (≥ 0)

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Uniform across renderers |

---

## Implementation Notes

- `frameCount` continues to increment when `redraw()` is called manually, even with `noLoop()` active.
- It does not increment while the loop is stopped via `noLoop()`.
- Useful as a time proxy for deterministic animation, but prefer `millis()` for real elapsed-time calculations since frame rate can vary.

---

## Pitfalls

- Using `frameCount` for time-based logic ties behavior to frame rate — if the sketch runs slower on another machine, animations will slow down proportionally. Use `millis()` for wall-clock time.
- `frameCount` is an `int` — it overflows at 2,147,483,647 frames (~414 days at 60 fps). Practically never an issue, but worth noting for long-running installations.
- Reading `frameCount` inside `setup()` always returns `0`, which can mislead initialization logic that depends on frame order.

---

## Examples

```processing
void setup() {
  size(600, 200);
  textSize(20);
}

void draw() {
  background(30);
  fill(255);
  text("Frame: " + frameCount, 20, 40);
  text("Time (millis): " + millis(), 20, 70);

  // Trigger an event every 60 frames
  if (frameCount % 60 == 0) {
    println("One second passed (approx)");
  }
}
```

```processing
// Deterministic animation using frameCount
void draw() {
  background(0);
  float x = width / 2 + cos(frameCount * 0.05) * 150;
  float y = height / 2 + sin(frameCount * 0.05) * 150;
  ellipse(x, y, 30, 30);
}
```

---

## Related Functions

- [`frameRate()`](frameRate.md)
- [`draw()`](draw.md)
- [`millis()`](../utilities/time/millis.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
