# `registerMethod()`

> **Category:** Core — Library API  
> **Status:** ✅ Complete

---

## Signature

```processing
void registerMethod(String methodName, Object target)
```

## Description

Registers a method on a target object to be called automatically at specific points in the Processing lifecycle. Used primarily by **library authors** to hook into the sketch loop without requiring users to call the library manually in `draw()` or event handlers.

The `methodName` string must match one of Processing's recognized lifecycle hook names.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `methodName` | `String` | — | Lifecycle hook: `"pre"`, `"draw"`, `"post"`, `"mouseEvent"`, `"keyEvent"`, `"dispose"` |
| `target` | `Object` | — | Object instance that contains the named method |

## Returns

`void`

---

## Lifecycle Hook Names

| Hook | Called |
|------|--------|
| `"pre"` | Before `draw()` each frame |
| `"draw"` | After the sketch's `draw()` each frame |
| `"post"` | After `draw()` and all registered draw hooks |
| `"mouseEvent"` | On any mouse event; method receives a `MouseEvent` parameter |
| `"keyEvent"` | On any key event; method receives a `KeyEvent` parameter |
| `"dispose"` | When the sketch exits (`exit()`) |

---

## Implementation Notes

- Methods registered with event hooks (`"mouseEvent"`, `"keyEvent"`) must accept the appropriate `processing.event.MouseEvent` or `processing.event.KeyEvent` parameter.
- Registered methods are called via reflection, so typos in `methodName` cause silent failures rather than compile errors.
- This API is intended for library code — sketches should use standard event handlers (`mousePressed()`, `keyPressed()`, etc.) instead.

---

## Pitfalls

- Registering the same method multiple times causes it to be called multiple times per frame/event — guard with a flag or call `unregisterMethod()` before re-registering.
- Registered `"draw"` hooks run on the animation thread alongside `draw()` — the same thread-safety rules apply.
- Typos in `methodName` fail silently — if your hook isn't being called, double-check the spelling.

---

## Examples

```processing
// Minimal library-style class that auto-updates each frame
class AutoUpdater {
  PApplet parent;
  int count = 0;

  AutoUpdater(PApplet p) {
    parent = p;
    p.registerMethod("draw", this);   // hook into the draw loop
    p.registerMethod("dispose", this);
  }

  void draw() {
    count++;
    // Library rendering here — called automatically each frame
  }

  void dispose() {
    println("AutoUpdater cleaned up after " + count + " frames");
  }
}

AutoUpdater au;

void setup() {
  size(400, 300);
  au = new AutoUpdater(this);
}

void draw() {
  background(30);
  fill(255);
  text("Frame via library: " + au.count, 20, 40);
}
```

---

## Related Functions

- [`unregisterMethod()`](unregisterMethod.md)
- [`exit()`](exit.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
