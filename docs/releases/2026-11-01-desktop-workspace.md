# Desktop workspace

The catalog previously kept a narrow mobile column on large screens. The desktop update introduces a side navigation rail and a wider workspace for product browsing, forms and dashboard tables. Dashboard section links open the relevant section and move keyboard focus to its heading.

The interface retains the application's typeface and existing dark palette. Mobile navigation stays in place. Access rules and business operations are unchanged.

Validation used the actual entry scripts with mocked API responses at mobile and two desktop widths, under both browser color preferences. Sixty-six browser assertions passed, including navigation and overflow checks. Existing ownership, guest-access and service-worker privacy checks also passed. Populated production data, authenticated writes and every administrative dialog remain outside this validation.

Released on 2026-11-01 with the notification center after owner approval. A backup and rollback procedure were prepared before deployment. Public asset hashes, the released entry version and unauthenticated API denial were verified. Live public-page checks passed at mobile and desktop widths without JavaScript errors or horizontal overflow. Authenticated business operations were not exercised.
