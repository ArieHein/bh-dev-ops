# Web UI Dashboard Component

## Purpose

- Show key project metrics for projects owned by the signed-in product owner.
- Provide quick access to favorite projects.

## Behavior

- Home dashboard shows projects owned by the signed-in product owner.
- Favorite project count has a configurable system limit.

## Data And Integration

- Uses project metadata and favorites from platform API and OpsDB.
- Requires fast summary views for dashboard cards and favorite project access.

## Persona Capability Coverage

| Capability | Workstream Product Owner | Workstream Developer | Workstream Manager | DevOps Team |
| --- | --- | --- | --- | --- |
| View summary of projects owned by | yes | no | yes | yes |
| View summary of projects member of | no | yes | yes | yes |
| View favorite projects | yes | yes | yes | yes |
| View projects metrics | yes | read-only | yes | yes |
| Add or remove project favorites | yes | yes | yes | yes |
