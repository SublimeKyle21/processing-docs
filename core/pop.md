# `pop()`

> **Category:** Core — Style & Transform Stack  
> **Status:** ✅ Complete

---

## Signature

```processing
void pop()
```

## Description

Restores the drawing state (transform matrix and style settings) previously saved with `push()`. Every `push()` must have a matching `pop()`. Equivalent to calling `popMatrix()` followed by `popStyle()`.

## Parameters

_None._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Uniform across renderers |

---

## Pitfalls

- Calling `pop()` without a preceding `push()` throws: `Too many calls to popMatrix()` (or similar) — always balance your stack.
- In loops, ensure every code path that calls `push()` eventually calls `pop()` — early `return` statements inside a push block are a common source of leaks.

---

## Examples

```processing
void draw() {
  background(20);
  for (int i = 0; i < 5; i++) {
    push();
      translate(100 + i * 80, height / 2);
      rotate(frameCount * 0.01 * (i + 1));
      fill(map(i, 0, 4, 50, 255), 100, 200);
      noStroke();
      rect(-20, -20, 40, 40);
    pop();
  }
}
```

---

## Related Functions

- [`push()`](push.md)
- [`popMatrix()`](../transforms/popMatrix.md)
- [`popStyle()`](popStyle.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
