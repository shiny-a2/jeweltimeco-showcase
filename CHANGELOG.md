# Changelog

## 2026-02-24
- Stabilized unique-code reservation flow for scanned orders.
- Added fallback behavior: when sampled/scanned unique code is not usable, system auto-reserves the first available unique code from the same order code.
- Improved resilience for mixed/legacy allocation table schemas (column and enum compatibility guards).
- Kept shortage behavior explicit: if inventory is exhausted, order lines are still captured with warning and without final unique code assignment.

## 2026-02-23
- Synced public documentation with latest private release baseline.
- Added product share capability notes (native share sheet + copy-link fallback).
- Added hardening notes for product-list return restore (cross-browser/PWA behavior).
- Updated version-control and release-tracking notes for cleaner operational history.

## 2026-02-22
- Initial public documentation-only release.
