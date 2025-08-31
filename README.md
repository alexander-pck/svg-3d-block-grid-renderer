3D Block Grid — test.html

Overview

This is a tiny orthographic SVG renderer (single file: `test.html`) that visualizes a grid of cubes and draws three screen-space brackets showing the grid dimensions:
- Height (Y) — vertical bracket
- Width (X) — horizontal bracket
- Depth (Z) — newly added depth bracket

All rendering is done in vanilla JavaScript. The cubes are placed in a simple world coordinate grid, rotated by theta (Y-axis) and phi (X-axis), projected into screen space and drawn as SVG polygons. Brackets are screen-space helpers attached to projected cube centers so they follow the visual outline of the grid.

Note on portability

- The project is primarily JavaScript-based and uses only basic DOM/SVG and math logic, so it is straightforward to adapt to React (including React Native SVG solutions), Vue, or other JS frameworks with minor modifications (wrapping rendering logic into components and routing input state through framework state management).

Controls (in-page)

- Width (X) — number of columns
- Height (Y) — number of rows / vertical layers
- Depth (Z) — number of depth layers
- Cube size (px) — size of each cube
- Margin (px) — spacing between cubes
- Theta (deg) — rotate around Y (left/right)
- Phi (deg) — rotate around X (up/down)
- Opacity (faces) — cube face opacity
- Border color — stroke color for cube faces
- Max visible slots — maximum visual slots per axis; if a dimension exceeds this the renderer shows markers (two dots) instead of the middle slot.

Visual helpers

- Brackets are drawn in SVG screen coordinates but anchored to projected cube centers so they appear attached to the visible edges of the grid.
- The width bracket picks a representative Y and Z layer depending on phi/theta to attach to the visually outer column and places the bracket outward along the perpendicular screen vector.
- The newly added depth bracket samples an X and Y layer (based on theta/phi) and draws a bracket between the front-most (z=0) and back-most (z=visD-1) projected centers, labeling it with the real `D` value.
- When a dimension is larger than `Max visible slots` the renderer uses `visW/visH/visD` for visual layout and shows a marker (two dots) in the middle slot to indicate omitted cells.

Implementation notes

- The input degrees for theta/phi are converted to radians internally (functions `deg()` and `rad()` exist). The code uses simple orthographic projection (no perspective).
- The bracket placement logic uses the sign of theta and phi to decide which side is visually outer; this keeps brackets readable and avoids overlapping with the grid.
- Colors for cube faces are computed from cube indices as an RGB mix for visual variety.

Troubleshooting

- If labels or strokes are hard to see, adjust `Border color` in the controls or increase `font-size` / `stroke-width` via the UI by changing `Cube size`.
- If a bracket is not where you expect, try changing `Theta`/`Phi` — the bracket chooses sampling axes based on those angles.

Examples & screenshot

- Live example: [Insert example URL here] (replace with your hosted `test.html` link)
- Screenshot: ![Screenshot placeholder](INSERT_SCREENSHOT_URL) (replace with path/URL to the screenshot you'll provide)

Customizing

- To change which cube column/row is used to anchor a bracket, edit the bracket IIFE near the end of `test.html`:
    - `drawHeightBracket` chooses a reference projected X column.
    - `drawWidthBracket` chooses a Y/Z layer.
    - `drawDepthBracket` chooses an X/Y layer (added in the file).

License

Use freely for prototypes and demos.
