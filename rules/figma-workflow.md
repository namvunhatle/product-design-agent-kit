# Figma workflow

Use this rule only in a project where the designer wants these canvas safety conventions. A request to review a design is read-only. Make Figma changes when the current request asks for them and the target is clear.

## Pin the file

Resolve one target file key and expected file name before the first Figma call. Pass the key explicitly to every supported call and inspect the returned file context. Do not rely on whichever file happens to be active in Figma. If the result names a different file, stop the run and report the last call and any writes already made. Do not continue in the newly active file.

Work in one Figma file per run. A second file needs a separate run with its own pinned key. If the current task needs information from both files, gather each file's evidence separately before planning a cross-file change.

## Before and after a write

Save a named version-history restore point before the first canvas write. Read the target section and its existing comments or review context. Keep the edit within the requested scope.

For a correction to an existing reviewed frame, edit the actual frame so comments and node references stay attached. For a new wireframe flow, create a new labeled section in empty canvas space. When a subagent is restricted to new sections, it must stop if the brief asks it to edit an older section.

An MCP timeout does not prove that a write failed. Read the file state before retrying a clone, import, transform, or delete. After a write, verify the affected nodes and capture a screenshot when visual output matters.

Figma MCP can inspect geometry and the reaction graph. It cannot play Present mode; ask the designer to judge motion in Figma before calling a prototype finished.
