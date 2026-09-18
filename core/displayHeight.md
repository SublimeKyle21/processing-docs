# `displayHeight`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
int displayHeight
```

## Description

The height of the primary display screen in pixels. Counterpart to `displayWidth`. See `displayWidth` for full details and pitfalls.

## Parameters

_System variable — not a function._

## Returns

`int` — primary display height in logical pixels

---

## Examples

```processing
void setup() {
  size(displayWidth, displayHeight - 80); // leave room for taskbar
}
```

---

## Related Functions

- [`displayWidth`](displayWidth.md)
- [`height`](height.md)
- [`fullScreen()`](fullScreen.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
