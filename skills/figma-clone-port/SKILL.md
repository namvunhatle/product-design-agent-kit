---
name: figma-clone-port
description: Port an existing Figma feature, component set, or prototype flow into another product file while preserving behavior and adapting to the destination design system. Use when the source design is already chosen; not for inventing a new flow.
metadata:
  author: namvunhatle
  version: 1.0.0
  mcp-server: figma-console
---

# Clone and port a Figma feature

Treat a port as an execution task. Preserve the source flow, copy, and interaction graph unless the designer asks for a change. Adapt the visual system and platform chrome to the destination file. Report any gaps in the source rather than silently redesigning them.

## Set the boundary before writing

1. Identify the source and destination file keys, names, pages, and sections. Pass the intended file key explicitly on every Figma MCP call and verify the returned file context. If the active file changes unexpectedly, stop the run and audit what happened before another write.
2. Read each file's local design rules. List the sections that are in scope and any reviewed sections that must remain untouched.
3. Map the source frames, components, reactions, variables, and modes. Save a named version-history restore point in the destination before the first write.
4. Build into a new destination section. Keep source nodes intact. When asked to modify an existing destination section, confirm its exact node IDs and work there only when the request calls for it.

## Port components and content

- Prefer components from the destination library. A cloned instance may still point to a source component, so inspect `getMainComponentAsync()` or the available component identity before and after a swap.
- Swap outer instances first; nested instances can be replaced along with their parent. Record component properties and text overrides by layer name before a swap, then reapply and verify them. A swap can reset overrides without an error.
- Preserve the source screen order and interface copy. Replace only destination-specific material such as system chrome, platform controls, and design tokens. Do not invent catalog items, names, metrics, or missing states.
- Convert repeated raw elements into local components only when the destination needs reusable states. Use variants or properties for real state differences; keep screen backgrounds on screens rather than inside reusable components.
- Measure alignment and spacing from the destination's established screens. Verify the same anchor values across corresponding frames.

## Map design tokens deliberately

Audit fills, strokes, typography, spacing, radius, and effects before binding. For every replacement that changes the visual result, record:

| Source value | Destination token | Visible change | Decision |
|---|---|---|---|
| example: 15 px label | example: 16 px text style | taller card | accept or keep local value |

Do not snap an unmatched value to a nearby token merely to increase token coverage. Calculate text contrast when a color substitution changes the foreground/background pair, and surface the tradeoff before committing that substitution.

Apply a variable mode at the intended section or frame ancestor once, then inspect inherited modes. Avoid stamping modes on every child or changing unrelated sections.

## Port the prototype graph

1. Extract every source reaction: trigger, destination, transition, duration, easing, and flow starting point.
2. Clone destination UI screens for the demo flow, then adapt interaction hotspots. Reactions copied with frames or buttons may create self-navigation; inspect them after each clone.
3. Keep matching animated layers at the same path across keyframes. Add invisible stand-ins only where Smart Animate needs the same layer on both sides.
4. Verify that every intended hotspot has one destination, every destination exists, and the flow has exactly one starting point. Read timeout values back; Figma may coerce unsupported values.
5. Inspect the final geometry and screenshots. Figma MCP cannot play Present mode, so ask the designer to judge the motion in Figma and name the beat that still needs visual review.

If animation is the main task, also load `figma-prototype-motion` when available.

## Handle uncertain writes

An MCP timeout does not prove the write failed. Read the destination state before retrying. Repeating a completed clone, import, or transform can duplicate objects or apply a change twice.

## Finish with evidence

Report the destination section and frame IDs, source-to-destination mapping, component references that remain external, token substitutions, reaction-graph checks, and anything not visually verified. Keep project-specific file keys and node IDs in the destination project's private documentation, not in this skill.
