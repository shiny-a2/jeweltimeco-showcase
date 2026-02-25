# Changelog

## 2026-02-25
- Added an operational hardening note for the plugin layer supporting the web app admin stack.
- Documented synchronized private releases:
  - `A2 Fast Archive Filters (MU) v1.3.8`
  - `A2 Order Fix Box (MU) v1.7.1`
  - `MU Admin + Action Scheduler Core v1.1.0`
  - `A2 CRM Plugin v3.2.1`
- Added a clear incident-to-mitigation summary for employer-facing review.
- Refined legacy plugin catalog references to English-only wording in `README.md` and `docs/PROJECT_INDEX.md`.
- Added two new private MU capabilities to public-safe platform documentation:
  - `A2 Security Malware Scanner (MU) v1.0.0`
  - `A2 Storage Audit & Log Writers (MU) v1.1.0`

## 2026-02-24
- Stabilized unique-code reservation flow for scanned orders.
- Added fallback behavior: when sampled/scanned unique code is not usable, system auto-reserves the first available unique code from the same order code.
- Improved resilience for mixed/legacy allocation table schemas (column and enum compatibility guards).
- Kept shortage behavior explicit: if inventory is exhausted, order lines are still captured with warning and without final unique code assignment.
- Added full transactional invoice editing in dashboard lists (admin/accountant): change customer, add/remove items, and edit quantities.
- Invoice customer reassignment now updates invoice ownership attribution cleanly for old/new customer views and aggregates.
- Reservation allocations are rebuilt during invoice edit save to keep unique-code inventory consistency.
- Excel invoice export remains synchronized because export is generated from current edited DB rows.

## 2026-02-23
- Synced public documentation with latest private release baseline.
- Added product share capability notes (native share sheet + copy-link fallback).
- Added hardening notes for product-list return restore (cross-browser/PWA behavior).
- Updated version-control and release-tracking notes for cleaner operational history.

## 2026-02-22
- Initial public documentation-only release.
