# DNS Provider Routing Pattern

This document defines zone-based DNS provider routing using provider-neutral commands.

## Implementation Timing Note

- Zone mappings and command examples in this document are illustrative patterns.
- Production mappings and module implementation details are defined after prioritized module list and database
  model are supplied.

## Neutral Command Surface

- `New-PlatformDnsRecord`
- `Get-PlatformDnsRecord`
- `Remove-PlatformDnsRecord`

Workloads call only neutral DNS commands.

## Provider Adapters

- Azure DNS adapter module:
  - wraps Azure DNS cmdlets
- ClouDNS adapter module:
  - wraps ClouDNS API since no PowerShell module is available

## Zone-Based Resolution Example

- `example.com` routes to `cloudns`
- `example-dev.com` routes to `azuredns`

The routing decision is driven by configuration values in OpsDB.

## Request Flow

1. Workload submits DNS request with zone and record details.
2. Resolver reads zone-to-provider mapping from OpsDB.
3. Neutral command routes request to selected adapter.
4. Adapter executes provider-native call.
5. Result is normalized and returned to caller.

## Governance And Safety

- Zone-to-provider mapping changes require approval and audit logging.
- Adapter credentials are managed securely and rotated per policy.
- Routing and execution events are logged with request ID and provider decision.

## Failure Handling

- Unknown zone mapping returns a policy error with remediation guidance.
- Provider API failures return normalized error codes for workflow handling.
- Retry behavior follows provider-specific safe retry rules.
