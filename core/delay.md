# `delay()`

> **Category:** Core — Control  
> **Status:** ✅ Complete

---

## Signature

```processing
void delay(int milliseconds)
```

## Description

Pauses execution for the specified number of milliseconds. When called on the main animation thread (i.e., inside `draw()`), it blocks the entire sketch — no frames are rendered and no events are processed during the pause. Its primary use case is inside methods invoked via `thread()` to simulate or throttle background work.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `milliseconds` | `int` | — | Duration to pause in milliseconds |

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Uniform — wraps `Thread.sleep()` |

---

## Implementation Notes

- Wraps `Thread.sleep(milliseconds)` and swallows the `InterruptedException`.
- On the main animation thread, blocks all rendering and input — the window appears frozen.
- On a background thread (spawned via `thread()`), safely pauses only that thread.

---

## Pitfalls

- **Never call `delay()` inside `draw()`** unless you intentionally want to freeze the sketch — it blocks the animation loop entirely.
- For timed events within `draw()`, use `millis()` comparisons instead:
  ```processing
  if (millis() - lastTime > 1000) { /* do something */ lastTime = millis(); }
  ```
- `delay()` is not a substitute for `frameRate()` — use `frameRate()` to control animation speed.

---

## Examples

```processing
// Safe use: inside a threaded method only
volatile String message = "Waiting...";

void setup() {
  size(400, 200);
  thread("pollServer");
}

void draw() {
  background(20);
  fill(255);
  textSize(20);
  textAlign(CENTER, CENTER);
  text(message, width / 2, height / 2);
}

void pollServer() {
  while (true) {
    delay(2000);   // wait 2s between polls
    message = "Polled at " + hour() + ":" + nf(minute(), 2) + ":" + nf(second(), 2);
  }
}
```

---

## Related Functions

- [`thread()`](thread.md)
- [`millis()`](../utilities/time/millis.md)
- [`frameRate()`](frameRate.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
