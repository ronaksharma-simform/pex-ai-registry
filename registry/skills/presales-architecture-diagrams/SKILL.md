---
name: presales-architecture-diagrams
description: Generate presales-grade architecture diagrams as standalone HTML/SVG files
stage: architecture
triggers:
  - architecture diagram
  - create a diagram
  - draw the architecture
  - system design visual
  - data flow diagram
  - integration workflow
  - technical visual
prerequisites: []
output_format: html
version: 0
---

# Presales Architecture Diagrams

## Overview

Produces a standalone, self-contained HTML file with embedded SVG architecture diagrams suitable for client presentations, proposals, and pitch decks. Every component justifies its presence, every technology choice is specific and defensible.

## Prerequisites

- Solution design document (if available) for component and technology context.
- Project brief or PRD for understanding system scope.

## Workflow

1. Identify all architectural layers (client, gateway, services, data, integrations, infrastructure)
2. Map specific technologies to each component from the solution design
3. Define data flow connections with protocol labels
4. Generate self-contained HTML with embedded SVG
5. Apply professional color-coded styling per layer
6. Add interactive tooltips for each component
7. Validate all components have specific labels (no generic names)

## Reference Files

- `references/svg-template.md` — SVG structure and styling guidelines

## Quality Gates

- [ ] All major components from solution design are represented
- [ ] No generic labels ("Service 1", "Database") — all have specific names/technologies
- [ ] Data flows labeled with protocol/pattern (REST, GraphQL, WebSocket, etc.)
- [ ] Diagram readable without zooming on 1440px screen
- [ ] HTML file is fully self-contained (no external dependencies)
- [ ] Color-coded layers with legend
- [ ] Interactive tooltips on hover

## Output Format

Save as `{ProjectName}_ArchitectureDiagram_v{Version}.html` in the outputs directory.
