# `pushStyle()`

> **Category:** Core — Style Stack  
> **Status:** ✅ Complete

---

## Signature

```processing
void pushStyle()
```

## Description

Saves the current style settings onto a stack. Style settings include: fill color, stroke color, stroke weight, stroke cap, stroke join, tint, color mode, text font, text size, text align, text leading, ellipse mode, rect mode, image mode, and blending mode. Restored with `popStyle()`.

Use `pushStyle()` / `popStyle()` (or the shorthand `push()` / `pop()`) to temporarily change style properties without affecting the surrounding drawing context.

## Parameters

_None._

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Uniform |

---

## Implementation Notes

- Does **not** save the transform matrix — use `pushMatrix()` or `push()` for that.
- Stack depth is the same as the matrix stack (~32 in Java2D).

---

## Pitfalls

- `pushStyle()` saves style state, not transformation state. Forgetting `pushMatrix()` alongside it when both are needed leads to transform bleed.
- Use `push()` / `pop()` instead of separate `pushMatrix()` + `pushStyle()` calls to reduce boilerplate and stack imbalance bugs.

---

## Examples

```processing
void draw() {
  background(40);

  // Default style
  fill(255);
  textSize(20);
  text("Normal text", 20, 40);

  pushStyle();
    fill(255, 100, 0);
    textSize(36);
    textAlign(CENTER);
    text("Big orange centered", width / 2, height / 2);
  popStyle();

  // Back to previous style
  text("Back to normal", 20, 80);
}
```

---

## Related Functions

- [`popStyle()`](popStyle.md)
- [`push()`](push.md)
- [`pop()`](pop.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
