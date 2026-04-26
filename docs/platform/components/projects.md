# Web UI Projects Component

## Purpose

- Provide project discovery and project-level navigation for visible projects.

## Behavior

- Shows all projects visible to the signed-in product owner.
  - By default all projects are internal so visible to all, unless the project owner marks the project as private.
  - Projects can be searched and filtered.
  - favorite projects will always appear first in the list.
- Allows users to mark projects as favorites.
- Favorite behavior:
  - favorites appear on the dashboard
  - favorite count is capped by platform policy
- Projects can be marked internal by a project owner to allow visibility to other product owners.
- Default visibility is private, meaning explicit invitation is required to view project details.

## Data And Integration

- Uses projects and project visibility APIs.
- Reads and updates favorites, visibility, and project metadata through platform services.

## Persona Capability Coverage

| Capability | Workstream Product Owner | Workstream Developer | Workstream Manager | DevOps Team |
| --- | --- | --- | --- | --- |
| View private projects (member) | yes | yes | yes | yes |
| View internal projects (cross-PO) | yes | yes | yes | yes |
| Search and filter projects | yes | yes | yes | yes |
| Mark project as internal | yes | no | yes | yes |
| Mark project as private | yes | no | yes | yes |
| Create new project | planned | no | no | planned |
