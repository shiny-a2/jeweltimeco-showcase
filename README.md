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

## Latest Public Update (2026-10-26)

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
