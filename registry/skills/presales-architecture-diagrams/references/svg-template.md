# SVG Architecture Diagram Template

## Structure

The HTML file must be fully self-contained with no external dependencies.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>{Project} — Architecture Diagram</title>
    <style>
      /* All styles inline — no external CSS */
    </style>
  </head>
  <body>
    <svg viewBox="0 0 1200 800" xmlns="http://www.w3.org/2000/svg">
      <!-- Layers, components, arrows, legend -->
    </svg>
    <div id="tooltip" class="tooltip"></div>
    <script>
      /* Tooltip interactivity — no external JS */
    </script>
  </body>
</html>
```

## Layer Colors (Brand-Aligned)

| Layer                  | Color  | Hex       |
| ---------------------- | ------ | --------- |
| Client / Frontend      | Blue   | `#3b82f6` |
| API / Gateway          | Purple | `#8b5cf6` |
| Backend Services       | Cyan   | `#06b6d4` |
| Database / Storage     | Amber  | `#f59e0b` |
| External APIs          | Green  | `#10b981` |
| Infrastructure / Cloud | Indigo | `#6366f1` |

## Component Style

- Rounded rectangles with 8px border-radius
- White text on semi-transparent colored background
- Technology name in bold, description below in smaller text
- Minimum 120px wide, 60px tall

## Arrow Style

- 2px stroke, slightly lighter than layer color
- Arrowhead marker at destination end
- Label centered on arrow path (protocol: REST, GraphQL, gRPC, WebSocket, AMQP, etc.)

## Tooltip

- Appears on component hover near mouse cursor
- Shows: component name, technology, brief description
- Dark background (#1e293b), white text, rounded corners
- Hidden by default, shown via JS mouseover events

## Layout

- Horizontal layers stacked vertically (top = client, bottom = infrastructure)
- Each layer is a semi-transparent band across full width
- Components spaced evenly within their layer
- Vertical arrows connect layers; horizontal arrows connect same-layer services

## Legend

- Bottom-right corner
- Small colored squares with layer name labels
- Semi-transparent background panel

## Responsive

- SVG uses viewBox for scaling
- Body has max-width: 1400px centered
- Font sizes use relative units within SVG
