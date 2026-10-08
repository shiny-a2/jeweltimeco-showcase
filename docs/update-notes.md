# Public Update Notes

## 2026-10-08 — Private management report access

- Restricted the JewelTime management assistant's menu, workbook intake, generated spreadsheets and competitor reports to private chats with explicitly allowlisted numeric Telegram identities.
- Removed username-based trust and silent-leak paths for unknown users and group chats.
- Added regression coverage for every configured administrator, unknown identities, username spoofing and group-chat denial; verified spreadsheet generation without sending live messages.

## 2026-10-01 — Readable price filters

- Group catalogue price-range amounts in threes while users type and accept Persian and Arabic digits.
- Send clean numeric values to the product filter and refresh the app's static-asset version.
- Verify amount parsing, source syntax and live asset delivery.

## 2026-10-02 — Marketplace availability contract

Corrected external stock synchronization to publish only available/unavailable values. Regression checks cover spreadsheet precedence, large batches, absolute stock writes, currency preservation and confirmed checkpoints. Provider price restrictions remain visible instead of being reported as successful changes. No production data or credentials are included in this showcase.

## 2026-10-03 — Marketplace price units

Corrected a tenfold price mismatch by converting the app's internal Rial amounts to Toman at the relevant marketplace boundary. Confirmed checkpoints retain the internal currency; previously queued work preserves its original units. Missing prices are skipped explicitly, and availability remains binary. Regression coverage includes complete batches, conversion, confirmation, operator access and private-request cache exclusions.

Live provider tracking confirmed every submitted valid price and availability operation after the correction. Missing-price rows remain explicitly incomplete. The earlier permission-only interpretation was superseded by this verified unit fix.
