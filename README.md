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

## Latest Public Update (2026-06-04)

- Expanded authorized bulk inventory and price update workflow to the sales consultant role.
- Added an in-dashboard sample file download so operators can create correctly structured upload files.
- Hardened upload handling so common header rows are ignored instead of becoming inventory data.
- Why it matters: stock and price maintenance can now happen closer to the sales workflow while reducing file-format mistakes.

## Portfolio

https://amiraliyaghouti.com
