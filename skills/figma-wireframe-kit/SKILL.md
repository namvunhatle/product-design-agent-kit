---
name: figma-wireframe-kit
description: Build or revise structural wireframes in Figma using the destination file's available wireframe kit or simple grayscale primitives. Use after the screen flow is defined; not for production visual design or prototype motion.
metadata:
  author: namvunhatle
  version: 1.0.0
  mcp-server: figma-console
---

# Figma wireframe kit

This is a public adaptation of a project-specific wireframe workflow. It contains no library component keys or project tokens. Discover those in the destination file at runtime.

## Before building

Read the brief, screen sequence, content requirements, and destination file's local rules. If multiple directions are still under comparison, use the `explore-vs-final` skill for construction fidelity. If the flow is unresolved, surface the decision before building screens.

Pin the target Figma file key and expected name. Pass the key on each supported call; inspect the returned file context. Save a named version-history restore point before the first write. Use a new section for a new flow and avoid changing reviewed sections outside the brief.

## Choose a construction source

If the destination has a wireframe kit, inspect the available components and their properties in that file. Do not paste keys from another file or assume a library is enabled. Search again when a component result is session-specific. If no kit is available, use consistent grayscale primitives and state that choice in the handoff.

Keep the wireframe structural: real screen order, believable content, clear interaction states, and enough detail to test the flow. Use low-fidelity styling so visual polish does not obscure an unresolved flow decision.

## Figma build checks

- Explicitly size new frames and containers. New Figma nodes can retain small defaults that make children overflow or collapse.
- Put a child inside its intended auto-layout parent before setting fill sizing, when the API requires that order.
- Inspect `clipsContent` on containers. A frame that looks fine at rest can crop content or motion later.
- Treat imported components as instances; use their exposed properties for labels and states. Verify overrides after a swap or bulk edit.
- Build in small sections, then measure frame height, overflow, alignment, and touch targets before screenshot review.
- If an MCP call times out, read the canvas before retrying. The write may already have completed.

Keep section labels concise and identify source, current option, and review state. Place comparison variants where the designer can inspect them together without altering the reviewed source.

## Deliver

Return the restore-point name, section and frame IDs, a screenshot, any components that stayed raw, and the flow questions that remain. Do not claim motion has been verified; Figma MCP cannot play Present mode.
