# Web UI Projects Component

## Purpose

- Provide project discovery and project-level navigation for visible projects.

## Behavior

- Shows all projects visible to the signed-in product owner.
- Supports search and filtering.
- Allows users to mark projects as favorites.
- Favorite behavior:
  - favorites appear on the dashboard
  - favorite count is capped by platform policy
- Projects can be marked internal by a project owner to allow visibility to other product owners.
- Default visibility is private, meaning explicit invitation is required to view project details.

## Data And Integration

- Uses projects and project visibility APIs.
- Reads and updates favorites, visibility, and project metadata through platform services.
