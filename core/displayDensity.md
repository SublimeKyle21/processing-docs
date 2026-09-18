# `displayDensity()`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
int displayDensity()
int displayDensity(int display)
```

## Description

Returns the pixel density of the specified display (or the primary display if no argument is given). On standard monitors returns `1`; on HiDPI/Retina displays returns `2`. Pass the result directly to `pixelDensity()` for automatic HiDPI support.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `display` | `int` | primary | Monitor number (1-based) to query |

## Returns

`int` — `1` for standard DPI, `2` for HiDPI/Retina

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| All | System query — renderer-independent |

---

## Pitfalls

- On Windows with fractional scaling (e.g., 125%, 150%), `displayDensity()` may return `1` even though the display is partially scaled — Processing does not expose fractional pixel ratios.
- Querying a non-existent display index returns `1` without throwing an error.

---

## Examples

```processing
void setup() {
  size(600, 400, P2D);
  pixelDensity(displayDensity());
  println("Pixel density: " + displayDensity());
}
```

---

## Related Functions

- [`pixelDensity()`](pixelDensity.md)
- [`displayWidth`](displayWidth.md)
- [`displayHeight`](displayHeight.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
