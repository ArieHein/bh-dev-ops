# Web UI People Component

## Purpose

- Provide project membership visibility and membership management workflows.

## Behavior

- Shows all platform users, default source is Microsoft Entra users.
- Users already assigned to owned projects are marked with project membership and role details.
- Product owners can invite users to projects they own and assign project roles.

## Data And Integration

- Uses people and project membership APIs.
- Depends on Microsoft Entra-backed identity data and role assignment workflows.

## Persona Capability Coverage

| Capability | Workstream Product Owner | Workstream Developer | Workstream Manager | DevOps Team |
| --- | --- | --- | --- | --- |
| View platform users | yes | yes | yes | yes |
| View project memberships | yes | yes | yes | yes |
| Invite user to owned project | yes | no | yes | yes |
| Assign project role to user | yes | no | yes | yes |
| Remove user from project | yes | no | yes | yes |
