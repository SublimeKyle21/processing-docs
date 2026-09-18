# `cursor()`

> **Category:** Core — Environment  
> **Status:** ✅ Complete

---

## Signature

```processing
void cursor()
void cursor(int kind)
void cursor(PImage img)
void cursor(PImage img, int hotspotX, int hotspotY)
```

## Description

Makes the mouse cursor visible and optionally changes its appearance. Calling `cursor()` with no arguments restores the default arrow cursor after `noCursor()` was called. Pass a `kind` constant to use a system cursor, or pass a `PImage` to use a custom cursor graphic.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `kind` | `int` | `ARROW` | System cursor type: `ARROW`, `CROSS`, `HAND`, `MOVE`, `TEXT`, `WAIT` |
| `img` | `PImage` | — | Custom cursor image (max 32×32 on most platforms) |
| `hotspotX` | `int` | `0` | X offset of the click point within the cursor image |
| `hotspotY` | `int` | `0` | Y offset of the click point within the cursor image |

## Returns

`void`

---

## Renderer Differences

| Renderer | Behavior |
|----------|----------|
| `default` (Java2D) | Full support for all overloads |
| `P2D` / `P3D` | Custom image cursors may be limited to 32×32 px due to LWJGL/JOGL cursor size restrictions |
| `FX2D` | System cursors work; custom image cursor size may vary |
| `PDF` / `SVG` | No cursor — these renderers produce file output, not interactive windows |

---

## Implementation Notes

- Custom cursor images larger than 32×32 pixels are silently clipped or rejected on many platforms — design custom cursors at exactly 32×32.
- `hotspotX` / `hotspotY` define which pixel of the image acts as the "click point." For a crosshair, use `(16, 16)` on a 32×32 image.
- Calling `cursor()` after `noCursor()` restores whichever cursor type was most recently set.

---

## Pitfalls

- Cursor images with transparency require a `PImage` with an alpha channel (PNG loaded with `loadImage()`).
- Passing an image larger than the platform limit causes a Java exception on some systems — always clamp to 32×32.
- System cursors (`HAND`, `TEXT`, etc.) look different on each OS — do not rely on a specific visual style.
- Calling `noCursor()` in `setup()` then `cursor()` in a mouse event handler is a common interactive pattern but can flicker in P2D/P3D.

---

## Examples

```processing
// Cycle through system cursor types on click
int[] cursors = { ARROW, CROSS, HAND, MOVE, TEXT, WAIT };
int idx = 0;

void setup() {
  size(400, 300);
}

void draw() {
  background(50);
  fill(255);
  textSize(18);
  text("Click to change cursor", 20, height / 2);
}

void mousePressed() {
  idx = (idx + 1) % cursors.length;
  cursor(cursors[idx]);
}
```

```processing
// Custom 32x32 crosshair cursor
PImage cur;

void setup() {
  size(600, 400);
  cur = createImage(32, 32, ARGB);
  cur.loadPixels();
  for (int i = 0; i < 32; i++) {
    cur.pixels[i * 32 + 16] = color(255, 0, 0);   // vertical bar
    cur.pixels[16 * 32 + i] = color(255, 0, 0);   // horizontal bar
  }
  cur.updatePixels();
  cursor(cur, 16, 16);   // hotspot at center
}
```

---

## Related Functions

- [`noCursor()`](noCursor.md)

---

*Last updated: 2026-09-17 · [Edit this page](https://github.com/SublimeKyle21/processing-docs)*
