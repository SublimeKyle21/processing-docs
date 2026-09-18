# Contributing to Processing Docs

## Filling in a Stub

1. Pick any `🔲 Stub` file.
2. Fill in all template sections (signature, description, parameters, returns, renderer differences, implementation notes, pitfalls, examples, related functions).
3. Change the status badge to `🟡 Partial` or `✅ Complete`.
4. Open a pull request — title format: `docs(category): fill functionName`.

## Template Sections

| Section | Notes |
|---------|-------|
| **Signature** | All overloads, each on its own code block |
| **Description** | What it does, when to use it, what not to do |
| **Parameters** | Every parameter with type, default, constraints |
| **Returns** | Return type and meaning |
| **Renderer Differences** | Java2D / P2D / P3D / PDF / SVG / FX2D |
| **Implementation Notes** | Internals, performance, platform quirks |
| **Pitfalls** | Bugs, unexpected behavior, common mistakes |
| **Examples** | At least one runnable sketch |
| **Related Functions** | Cross-links to sibling docs |

## Batch Plan

Planned fill order:
1. `core/` — lifecycle and environment
2. `shapes/2d-primitives/` — most-used drawing functions
3. `transforms/` — matrix stack
4. `graphics/color/` — color model and fill/stroke
5. `math/` — all sub-categories
6. `images/` — pixel and image ops
7. `text/` — typography
8. `io/` — file I/O
9. `lighting/` + `shaders/` — 3D pipeline
10. `renderers/` — off-screen buffers
11. `sound/` — Sound library
12. `utilities/` — all sub-categories
13. `pitfalls/` — cross-cutting concerns
14. `examples/` — annotated sketches
