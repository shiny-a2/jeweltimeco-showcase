# Customer workflow correction — prepared

Existing customer selection and profile updates could be blocked when the assigned sales consultant differed from the current staff member. A prepared correction lets authorized staff reuse the existing contact, update its current advisor and submit an invoice with consistent sales attribution. Earlier invoices retain their recorded attribution.

The forms reject stale lookup responses, show useful save errors and preserve a newly opened dialog when the previous one finishes closing. Customer and guest boundaries remain explicit, while private customer files keep their existing authorization checks. No schema migration, service or provider integration is added.

Validation uses synthetic data: 64 backend checks cover the real contact/invoice SQL, rollback, advisor changes, role denial and endpoint behavior. Eighty browser checks cover the changed forms at mobile and desktop widths under light and dark browser preferences, retaining the app's existing dark palette. Checks include keyboard focus, readable text and placeholders, touch controls, lookup races, save failures and invoice finalization. Additional isolated compatibility checks cover the existing inventory/price guards and notification routing without external delivery. Existing export, notification, marketplace and private-cache regressions pass; the desktop smoke suite also passes. Screenshots were inspected privately.

This records implemented and locally tested work. Production activation and authenticated acceptance remain pending. No real invoice, customer message or financial test record was created.
