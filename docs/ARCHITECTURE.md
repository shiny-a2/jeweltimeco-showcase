# Architecture

High-level architecture:

- Presentation: vanilla JS front-end and PWA shell.
- Application: PHP service layer for auth, workflows, and role-based operations.
- Data: MySQL domain schema with WooCommerce read-integration boundary.
- Messaging: OTP/SMS and push notification pipeline.

Design emphasis:
- Role-aware operational journeys.
- Progressive enhancement for mobile-first usage.
- Reliability-first integration boundaries with existing commerce data.
