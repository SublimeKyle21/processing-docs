# `push()`

> **Category:** Core — Style & Transform Stack  
> **Status:** ✅ Complete

---

## Signature

```processing
void push()
```

## Description

Saves the current drawing state (transform matrix **and** style settings) onto a stack, to be restored later with `pop()`. Introduced in Processing 3.5 as a convenient shorthand for calling both `pushMatrix()` and `pushStyle()` in one call.

Use `push()` / `pop()` to isolate transformations and style changes to a block of drawing code without affecting the rest of the sketch.

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

## Implementation Notes

- `push()` is exactly equivalent to calling `pushMatrix()` followed by `pushStyle()`.
- The stack depth is limited to 32 levels in Java2D and effectively unlimited in P2D/P3D (OpenGL matrix stack). Exceeding 32 levels in Java2D throws a runtime error.
- `push()` / `pop()` pairs must be balanced — an unmatched `push()` leaks state onto the stack and an unmatched `pop()` throws an error.

---

## Pitfalls

- Nesting more than ~32 `push()` calls deep in Java2D causes "matrix stack overflow" — restructure deeply recursive drawing code.
- Forgetting `pop()` after `push()` in a conditional block leaves the stack unbalanced — transforms bleed into subsequent frames.
- `push()` / `pop()` do **not** save/restore the pixel buffer — only matrix and style state.

---

## Examples

```processing
void draw() {
  background(30);

  // Isolated red rotated square
  push();
    fill(255, 60, 60);
    translate(200, 200);
    rotate(frameCount * 0.02);
    rect(-40, -40, 80, 80);
  pop();

  // This ellipse is unaffected by the rotation above
  fill(60, 180, 255);
  ellipse(400, 200, 60, 60);
}
```

```processing
// Recursive tree using push/pop
void branch(float len) {
  line(0, 0, 0, -len);
  translate(0, -len);
  if (len > 10) {
    push();
      rotate(PI / 6);
      branch(len * 0.67);
    pop();
    push();
      rotate(-PI / 6);
      branch(len * 0.67);
    pop();
  }
}

void setup() {
  size(600, 600);
  background(20);
  stroke(200, 160, 80);
  translate(width / 2, height);
  branch(120);
  noLoop();
}
```

---

## Related Functions

- [`pop()`](pop.md)
- [`pushMatrix()`](../transforms/pushMatrix.md)
- [`popMatrix()`](../transforms/popMatrix.md)
- [`pushStyle()`](pushStyle.md)
- [`popStyle()`](popStyle.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
