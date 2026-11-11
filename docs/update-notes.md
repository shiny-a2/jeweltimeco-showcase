# Public Update Notes

## 2026-11-11 — Corporate multi-brand storefront

The public WooCommerce homepage previously centered a single watch and shopping message. It now introduces JewelTime as a company with multiple watch brands, gives each of ten brand pages a clear entry point, and makes the catalogue and representation form easier to find. Navy and gold follow the existing site identity, while product photography stays in the catalogue section.

The live homepage was inspected at mobile and desktop widths in light and dark browser preferences. The brand links, navigation, search focus, form presence, Persian file-selection text and horizontal overflow were checked. No purchase or inquiry was created. This storefront is separate from the operations app described in the other updates.

## 2026-11-11 — Consistent brand labels across catalog workflows

Some imported watches carried an order code but no brand, leaving operational spreadsheets incomplete. The export flow now fills a missing brand only when the code prefix has one verified meaning. The import flow assigns an eligible watch's existing brand and category terms without replacing a conflicting explicit value. A dry-run-first, recoverable repair handled one previously published item.

Focused export and import checks passed. A live read-only export-row check and a public desktop product-page check showed the expected brand. Authenticated file download and mobile or alternate-theme visual states remain outside the completed checks.

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
