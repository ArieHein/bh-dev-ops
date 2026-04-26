# Provider-Neutral Module Pattern

This pattern defines the internal module buffer model for platform automation.

## Implementation Timing Note

- Examples in this document are reference patterns for engineering design.
- Concrete module command catalogs and implementation contracts are deferred until prioritized module list is
  provided by platform leadership.

## Why This Exists

- Workloads should call stable platform commands and not vendor-specific commands directly.
- Vendor migration should not require broad caller changes.
- Provider-specific implementation is isolated behind adapter modules.

## Core Rule

- Callers use provider-neutral commands, for example `Get-PlatformVM`.
- Internal adapter modules translate neutral commands to provider-native operations.

Examples:

- `Get-PlatformVM` can route to VMware `Get-VM` or Azure `Get-AzVM`.
- Caller behavior remains stable when platform provider strategy changes.

## Architecture Model

- Workload layer:
  - calls neutral commands only
- Orchestration layer:
  - resolves provider from explicit input or configuration store (OpsDB)
  - applies policy and validation
- Provider adapter modules:
  - one adapter per provider and capability domain
  - wraps native APIs or cmdlets

## Provider Resolution

Provider resolution supports two paths:

1. Request-provided provider
2. Configuration-driven provider resolved from OpsDB

Configuration examples:

- global defaults by capability
- environment-specific provider
- zone-specific provider
- workload-specific override

## Command Contract Guidelines

- Neutral command naming uses `Platform` prefix, for example `Get-PlatformVM`.
- Input contract must be provider-agnostic.
- Output contract must be normalized across providers.
- Provider-specific metadata is allowed in an extension field without breaking core contract.

## Migration Benefit

- Migrating from one provider to another is mostly adapter-module work.
- Most workload scripts remain unchanged.
- Testing effort focuses on adapter parity and contract conformance.

## Testing Requirements

- Contract tests for neutral command input and output.
- Adapter tests for each provider implementation.
- Routing tests for provider resolution logic.
- Regression tests to confirm caller workflows remain unchanged after provider swap.
