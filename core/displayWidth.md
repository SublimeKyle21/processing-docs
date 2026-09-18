# `displayWidth`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
int displayWidth
```

## Description

The width of the primary display screen in pixels. Available at any point in the sketch — even before `size()` is called — making it useful for dynamically sizing the canvas relative to the screen.

On multi-monitor setups, `displayWidth` reflects the primary monitor. Use `displayWidth` inside `size()` to create a borderless or near-fullscreen window.

## Parameters

_System variable — not a function._

## Returns

`int` — primary display width in logical pixels

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | Same value regardless of renderer |

---

## Pitfalls

- On multi-monitor setups, `displayWidth` always reports the **primary** monitor — there is no built-in way to query secondary monitors in standard Processing.
- On HiDPI/retina displays, `displayWidth` may report the logical resolution (e.g., 1440) rather than the physical pixel count (e.g., 2880) depending on the OS scaling setting.

---

## Examples

```processing
void setup() {
  // Half the screen width, full height
  size(displayWidth / 2, displayHeight);
}

void draw() {
  background(0);
  fill(255);
  text("Screen: " + displayWidth + " x " + displayHeight, 20, 30);
}
```

---

## Related Functions

- [`displayHeight`](displayHeight.md)
- [`width`](width.md)
- [`fullScreen()`](fullScreen.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
