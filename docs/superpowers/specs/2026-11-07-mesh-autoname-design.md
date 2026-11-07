# Mesh Autoname Design

## Goal

Make export autonaming use the active mesh datablock name by default, while
retaining the existing preference as an opt-out.

## Behavior

- The autoname preference defaults to enabled.
- When enabled, the export filename stem comes from
  `context.active_object.data.name`.
- Existing filename sanitization remains unchanged.
- An empty sanitized name continues to fall back to `mesh`.
- When disabled, the existing blend-file/path-derived filename remains in use.
- Preference labels and descriptions refer to the mesh name rather than the
  object name.

## Implementation

Update the export operator's autoname branch in `io_export_o3d/__init__.py`
to read the active object's mesh datablock name. Change the
`use_object_name` property default to `True` and update its user-facing
wording. No new abstraction or dependency is needed.

## Validation

Review the resulting diff for the exact source and default-value changes, then
run the repository's available checks. Since the repository does not include a
Blender test harness, validation will also include syntax/static inspection of
the modified Python module.
