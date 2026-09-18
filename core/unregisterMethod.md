# `unregisterMethod()`

> **Category:** Core — Library API  
> **Status:** ✅ Complete

---

## Signature

```processing
void unregisterMethod(String methodName, Object target)
```

## Description

Removes a previously registered lifecycle hook from the Processing event system. Call this when a library object is no longer needed, to stop its callbacks from firing and to allow it to be garbage collected.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `methodName` | `String` | — | Hook name matching the original `registerMethod()` call |
| `target` | `Object` | — | The same object instance that was registered |

## Returns

`void`

---

## Pitfalls

- Calling `unregisterMethod()` with a `target` that was never registered is a no-op — no error is thrown.
- Forgetting to unregister objects before discarding them keeps them alive in the Processing callback list (memory leak) and continues calling their methods unnecessarily.

---

## Examples

```processing
class Particle {
  PApplet p;
  boolean alive = true;

  Particle(PApplet p) {
    this.p = p;
    p.registerMethod("draw", this);
  }

  void draw() {
    if (!alive) {
      p.unregisterMethod("draw", this);
      return;
    }
    p.ellipse(p.random(p.width), p.random(p.height), 5, 5);
  }

  void kill() { alive = false; }
}

Particle pt;

void setup() {
  size(400, 400);
  pt = new Particle(this);
}

void draw() {
  background(20);
}

void mousePressed() {
  pt.kill();   // stops drawing and unregisters itself
}
```

---

## Related Functions

- [`registerMethod()`](registerMethod.md)
- [`exit()`](exit.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
