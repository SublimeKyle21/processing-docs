# `frameRate()`

> **Category:** Core — Lifecycle  
> **Status:** ✅ Complete

---

## Signature

```processing
void frameRate(float fps)
```

## Description

Sets the target number of frames per second that `draw()` should be called. Processing defaults to 60 fps. The actual frame rate may be lower if `draw()` takes longer than the allotted frame period, or slightly different due to OS scheduling.

The current achieved frame rate is available via the `frameRate` variable (note the case difference).

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `fps` | `float` | `60` | Target frames per second. Values ≤ 0 are ignored. |

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `default` (Java2D) | Uses `Thread.sleep()` for timing; subject to JVM scheduling jitter |
| `P2D` / `P3D` | Syncs with display vsync when possible; actual cap is the monitor refresh rate |
| `FX2D` | Tied to JavaFX animation timer; 60 fps is the practical ceiling on most displays |
| `PDF` / `SVG` | Frame rate has no visual effect; each `draw()` still appends output |

---

## Implementation Notes

- Call `frameRate()` inside `setup()` or inside `draw()` — both are valid.
- Setting a very high value (e.g., `frameRate(10000)`) effectively removes the cap, but the actual rate is limited by `draw()` complexity and OS scheduling.
- The `frameRate` variable (read-only, lowercase) is a smoothed exponential moving average of recent frame durations — it lags behind sudden changes.

---

## Pitfalls

- `frameRate()` is a **target**, not a guarantee. Heavy sketches will drop below the target rate.
- Using `frameRate()` to control animation timing is brittle — use `deltaTime` or `millis()` for time-based movement instead.
- Calling `frameRate(0)` or a negative value is silently ignored; the last valid rate persists.
- On retina/HiDPI displays with P2D/P3D, the effective frame rate may be capped at the display's native refresh rate regardless of what you set.

---

## Examples

```processing
void setup() {
  size(400, 400);
  frameRate(30);   // slow down for generative art
}

void draw() {
  background(20);
  fill(255);
  textSize(16);
  text("fps: " + nf(frameRate, 1, 1), 10, 20);
  ellipse(random(width), random(height), 10, 10);
}
```

```processing
// Time-based movement — preferred over frame-rate-dependent movement
float x = 0;
float speed = 200; // pixels per second

void draw() {
  background(40);
  x += speed * (deltaTime / 1000.0);  // deltaTime in ms (Processing 4+)
  if (x > width) x = 0;
  ellipse(x, height / 2, 30, 30);
}
```

---

## Related Functions

- [`frameCount`](frameCount.md)
- [`draw()`](draw.md)
- [`loop()`](loop.md)
- [`noLoop()`](noLoop.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
