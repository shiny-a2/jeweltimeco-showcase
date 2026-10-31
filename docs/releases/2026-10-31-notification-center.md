# Notification center — prepared release

A persistent inbox brings order updates and relevant notices into one place. A header badge shows unread messages; users can browse history, filter unread items, mark visible messages as read and follow an internal link to the related section. Phone notification settings stay in a separate, collapsed section.

Receiving a push notification does not mark the message as read. The inbox checks the signed-in recipient before reading or acknowledging messages. Existing notification producers remain unchanged.

Validation includes sixteen database behavior checks through a SQLite adapter, a guest-denial check, forty synthetic browser checks and integration of the actual app entry, route and header at mobile and desktop widths. The read query was also checked against MariaDB. Live write/concurrency acceptance remains pending. The app's existing dark palette is preserved under both browser color preferences.

The feature is committed and prepared; production deployment is awaiting owner approval. No customer broadcast or test purchase was generated.

## Release update

Published on 2026-11-01 together with the desktop workspace after owner approval. Public assets and unauthenticated API denial were verified. Authenticated read-state changes remain outside the production checks; the preparation-stage validation above used controlled fixtures.
