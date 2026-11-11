# JewelTimeCo Showcase

Project Status: Public architecture overview

This repository is a narrowed, public-safe architecture overview for a retail operations web app concept covering catalog browsing, assisted ordering, role-based dashboards, inventory handling, customer workflows, and internal operations.

## Public Scope

The repository should explain the shape of the system without exposing implementation details that could affect a real business operation.

Safe to discuss:

- high-level architecture;
- role and workflow categories;
- operational constraints;
- public-safe diagrams;
- anonymized engineering decisions.

Not safe to publish:

- production source code;
- private customer/order data;
- provider credentials;
- internal endpoints;
- route tables;
- operational logs;
- sensitive business procedures.

## Recommended Position In Portfolio

This repo is useful as a secondary platform architecture signal. It should not outrank the core WooCommerce infrastructure repos in the pinned profile.

## Latest Public Update (2026-11-12)

The lower homepage now moves directly from available brand models to four clearly grouped video links and a more compact agency form. The video label and form introduction are clearer, the form uses two columns on desktop and one on mobile, and the footer no longer shows social icons without destinations. The working trust and credit links remain. Live checks covered the lower page at mobile and desktop widths in light and dark preferences, including brand selection, carousel movement and file selection; no form was submitted. The shop, product and account entry also loaded after publication.

## Previous Storefront Update (2026-11-12)

The storefront homepage now leads with JewelTime's own logo and the slogan «زمان جواهر است». Brand model carousels display current public catalogue prices or an inquiry label when a price is absent. The shop shows all ten brand logos in a complete desktop grid, the desktop header stays on one line, brand archives offer gender paths, and the product layout keeps its specifications within the page at intermediate widths. The legacy login route leads to the existing account form. Live checks covered the homepage, shop, brand archive, product and account entry at mobile and desktop widths in light and dark preferences; the product was also checked at an intermediate width. Product gallery and account password visibility controls worked. Authenticated account pages were not tested; no purchase, message or login was submitted.

## Previous Storefront Update (2026-11-12)

The JewelTime storefront now pairs its corporate brand directory with official watch campaign imagery, including Tornado's red-car watch banner. Brand logos open the available women's and men's models in manually controlled carousels, and brand pages use matching campaign imagery where verified assets were available. The live homepage, brand archive, shop and contact pages were checked at mobile and desktop widths in both browser color preferences. Catalogue data and commerce operations remain in their existing systems; no purchase or inquiry was submitted.

## Previous Storefront Update (2026-11-11)

The separate public WooCommerce storefront now presents JewelTime as a multi-brand watch company. Its homepage leads with the company and a ten-brand index, followed by catalogue and representation paths. The existing agency form has a cleaner visual treatment and Persian file-selection text. The live page was checked on mobile and desktop in both browser color preferences, including navigation, search focus and file selection; no order or inquiry was submitted.

The operations app update below remains independent of the storefront work.

## Previous Update (2026-11-11)

Catalog exports now resolve a missing watch brand from an unambiguous brand-specific order-code prefix. The same brand decision is used in product, stock and marketplace spreadsheets. An import guard also fills missing brand and category data for eligible watches while preserving explicit conflicting values; a scoped repair corrected one existing published product after a dry run and private recovery snapshot.

Focused checks passed and a live read-only export-row check returned the expected brand. The public desktop product page showed the brand and category. An authenticated spreadsheet download and mobile or alternate-theme visual states were not verified.

## Previous Update (2026-10-26)

Recently imported products had valid warehouse and price records but were missing from the app because their storefront categories were incomplete. A scoped reconciliation restored their existing categories and missing prices, making the completed imports visible across the connected catalogs.

The repair checked product identity before writing, kept private recovery snapshots and verified saved values without changing stock. Production catalog and synchronization readbacks confirmed the result. Browser checks covered product images, displayed prices and app search on mobile and desktop; no real order or customer message was created for testing.

## Previous Update (2026-10-12)

- Added a controlled price-only release workflow for six watch brands across an operations app, two storefronts and connected marketplaces.
- Existing promotional percentages can be recalculated against the new list prices where approved.
- The workflow validates source prices, preserves stock, records private rollback snapshots and tracks marketplace confirmations before marking them complete.
- The six-brand production rollout was checked against storefront prices and completed marketplace confirmations.
- Why it matters: a supplier price change can be applied consistently without turning a pricing task into an inventory change.

## Previous Update (2026-10-08)

- The management assistant now keeps every workbook and report route inside private, numeric-ID administrator access.
- Unknown users, username impersonation and group chats cannot receive management prompts or generated files.
- Regression and live read-only checks cover access decisions and valid spreadsheet generation.
- Why it matters: operational exports remain available to the approved team without exposing private business data through the bot.

## Portfolio

https://amiraliyaghouti.com
