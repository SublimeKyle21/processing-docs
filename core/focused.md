# `focused`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
boolean focused
```

## Description

A built-in boolean variable that is `true` when the sketch window has keyboard focus, and `false` when the window is in the background or another application has focus. Useful for pausing animation or ignoring input events when the sketch loses focus.

## Parameters

_System variable — not a function._

## Returns

`boolean` — `true` if the sketch window is focused

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Reflects OS window focus state; behavior is consistent across renderers |

---

## Pitfalls

- In some environments (fullScreen mode, kiosk installations), `focused` may always be `true` because the window is always in front.
- On macOS, switching to another Space can set `focused = false` even if the sketch window is visible.

---

## Examples

```processing
void draw() {
  if (focused) {
    background(30);
    fill(0, 255, 100);
    text("Active", 20, 40);
  } else {
    background(80);
    fill(200);
    text("Paused — click to resume", 20, 40);
  }
}
```

---

## Related Functions

- [`draw()`](draw.md)
- [`loop()`](loop.md)
- [`noLoop()`](noLoop.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
