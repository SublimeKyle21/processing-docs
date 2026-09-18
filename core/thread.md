# `thread()`

> **Category:** Core — Control  
> **Status:** ✅ Complete

---

## Signature

```processing
void thread(String methodName)
```

## Description

Runs a method defined in the sketch on a new background thread. The named method must have the signature `void methodName()` — no parameters, no return value. Use `thread()` to offload slow operations (network requests, file I/O, heavy computation) without blocking the `draw()` loop.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `methodName` | `String` | — | Name of a zero-argument `void` method in the sketch to run on a new thread |

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Threading behavior is JVM-level; renderer-independent |

---

## Implementation Notes

- Uses Java reflection to find and invoke the named method on a new `java.lang.Thread`.
- The spawned thread runs concurrently with `draw()` — shared variables must be declared `volatile` or access must be `synchronized` to avoid race conditions and visibility issues.
- Each call to `thread()` creates a new `Thread` object — repeated calls (e.g., every frame) will create thousands of threads. Call it once or guard with a flag.
- For more control over threading (thread pools, futures, cancellation), use Java's `java.util.concurrent` package directly.

---

## Pitfalls

- Calling drawing functions (`fill()`, `ellipse()`, etc.) from inside a threaded method is **not thread-safe** and will cause crashes or corrupted output — only call draw functions from `draw()`.
- Spawning a new thread every frame via `thread("myMethod")` inside `draw()` is a resource leak and will eventually crash the JVM with an `OutOfMemoryError`.
- No built-in mechanism exists to cancel a running thread created by `thread()` — design the method to check a `volatile boolean running` flag and exit cleanly.
- Exceptions thrown inside the threaded method are swallowed silently unless you add a try/catch block inside the method.

---

## Examples

```processing
// Load data in background without blocking draw()
volatile String status = "Loading...";
volatile float[] data = null;

void setup() {
  size(600, 300);
  textSize(18);
  thread("loadData");   // fire and forget
}

void draw() {
  background(30);
  fill(255);
  text(status, 20, 50);
  if (data != null) {
    for (int i = 0; i < data.length; i++) {
      float x = map(i, 0, data.length - 1, 20, width - 20);
      line(x, height, x, height - data[i] * height);
    }
  }
}

void loadData() {
  delay(1500);   // simulate slow network/disk
  data = new float[50];
  for (int i = 0; i < data.length; i++) data[i] = random(1);
  status = "Done — " + data.length + " points loaded";
}
```

---

## Related Functions

- [`delay()`](delay.md)
- [`frameRate()`](frameRate.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
