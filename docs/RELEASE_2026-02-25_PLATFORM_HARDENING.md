# Platform Hardening Release — 2026-02-25

## Why This Update Mattered
A backend admin incident blocked a business-critical SEO flow (`Add New Redirection` in Rank Math).  
The same release window also contained reliability issues tied to host-alias admin AJAX routing and broader-than-needed admin asset loading.

## Private Release Synchronization
- `A2 Fast Archive Filters (MU)` -> `v1.3.8`
- `A2 Order Fix Box (MU)` -> `v1.7.1`
- `MU Admin + Action Scheduler Core` -> `v1.1.0`
- `A2 CRM Plugin` -> `v3.2.1`

## Technical Remediation Summary
- Added compatibility guards for redirections field payload defaults.
- Added same-origin normalization for admin AJAX endpoint usage.
- Prevented duplicate redirections runtime load on the same admin screen.
- Restricted order-fix admin assets to relevant order screens.
- Hardened typed price inputs in archive filtering to prevent invalid states.

## Operational Impact (Anonymized)
- Restored blocked SEO admin operations without rollback.
- Reduced recurrence risk for runtime collisions and host-alias AJAX failures.
- Improved release traceability with explicit version bumps and taggable rollback points.

## Verification Snapshot
- PHP syntax checks passed on all updated PHP modules.
- Browser console validation passed for redirections runtime and hook registration.
- Functional smoke checks passed on:
  - redirections creation flow,
  - CRM admin notifications,
  - order admin operations,
  - archive filter input handling.

## Public Safety
This note intentionally excludes customer data, credentials, and private implementation details.
