---
name: figma-design-system-ui
description: Build production UI in Figma from the destination file's existing design system, using live component and variable discovery. Use for approved visual designs and handoff-ready screens; not for grayscale wireframes or edits to the shared library itself.
metadata:
  author: namvunhatle
  version: 1.0.0
  mcp-server: figma-console
---

# Figma design-system UI

This is a public adaptation of a project-specific production UI workflow. Query the destination design system live. No component keys, mode IDs, or token values are bundled here.

## Decide the track

Confirm that the task calls for approved visual UI rather than a wireframe or an option still being compared. Read the product brief, approved direction, existing screens, and design-system guidance. Map the screens and states before writing. If a visual choice remains open, present the decision and its tradeoffs instead of encoding a guess as production UI.

Pin the target file key and expected name on every supported Figma MCP call. Save a named version-history restore point before the first write. Treat a shared library as read-only unless the user explicitly requested work in that library.

## Discover the system

Inspect the destination's available component sets, variants, text styles, variable collections, and modes. Library keys may be stable across a library while enablement differs by consuming file; verify access in the target file. Set the appropriate mode once on the intended outer container, then inspect inheritance. Avoid stamping modes on every child.

Use semantic tokens where the system provides them. Query current values rather than trusting a copied token sheet. Bind color, typography, spacing, radius, and effect values where the API and design system support them. Record justified local values instead of snapping to a nearby token that changes layout or contrast.

## Build and verify

- Start from the existing screen shell and component patterns when they fit. Use component properties and variants for real states; do not imitate them with detached lookalikes without a reason.
- Measure alignment and spacing numerically across related screens. A visually close but inconsistent grid is still a mismatch.
- Check content length, loading, error, empty, and selected states that the brief requires.
- Verify variable bindings and component references after a build. A matching hex color alone does not prove a semantic token is bound.
- Capture screenshots at meaningful checkpoints, inspect the actual pixels, and repair visible clipping, overlap, contrast, or hierarchy problems.
- A timeout may occur after the write completed; inspect state before retrying.

For token substitutions that visibly change the source, report `old value → token → visual difference → decision`. Finish with section and frame IDs, binding coverage, deliberate exceptions, screenshots, and anything still awaiting the designer's judgment.
