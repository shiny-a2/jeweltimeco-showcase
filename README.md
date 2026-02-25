# JewelTime WebApp Showcase

Public-safe, full capability documentation for the JewelTime production web app.
This README intentionally includes feature and architecture details, but no secrets.

## Operational Hardening Update (2026-02-25)
- Added two shared-host diagnostics modules to private operations stack:
  - A2 Security Malware Scanner (MU) v1.0.0
  - A2 Storage Audit & Log Writers (MU) v1.1.0

- Resolved an admin runtime conflict that blocked SEO redirection authoring in the WordPress backend.
- Hardened same-origin admin AJAX behavior for host-alias reliability.
- Tightened plugin asset scoping in admin order workflows to reduce cross-module collisions.
- Synchronized private plugin releases and documented rollout details in:
  - `docs/RELEASE_2026-02-25_PLATFORM_HARDENING.md`

## 1) Product Definition

JewelTime WebApp is a Persian/RTL, mobile-first **PWA** that combines:

- Product catalog browsing
- Sales ordering workflow (pre-invoice to fulfillment)
- CRM-lite (customers, consultants, files, communication history)
- Role-based operational dashboards
- Inventory allocation by unique barcode-level stock
- Admin communication center (push + SMS + logs)

It is not only a storefront; it is a complete operational system for sales, accounting, and management workflows.

## Latest Public Update (2026-02-25)
- Fixed false out-of-stock visibility in product list/search/detail when products contain multiple order-code attributes.
- Added robust order-code selection logic to prefer codes with real available inventory.
- Product trace panel upgraded with dual lookup modes:
  - Unique-code trace (single unit-level status and invoice context).
  - Order-code trace (all related invoices/customers for the same product code).
- Added order-code sales visibility in trace results:
  - Invoice number, status, customer, consultant, quantity, and line totals.
- Added inventory summary block in order-code trace:
  - Total, reserved, consumed, and available counts.
- Reservation lifecycle behavior documented and aligned with operations:
  - Reserve on order submit/edit.
  - Consume only when both conditions are met: status becomes `invoiced` and accounting invoice number is present.

## 2) Technology Stack

- Backend: PHP (procedural endpoints + shared libs)
- Database: MySQL/MariaDB
- Dual DB model:
- WooCommerce DB (catalog/media/taxonomy source + stock/price sync target)
- App DB (users, customers, orders, statuses, files, inventory, notifications, logs)
- Frontend: Vanilla JavaScript SPA (`assets/app.js`) + hash router
- UI: Custom CSS + Jalali date picker (Persian calendar)
- PWA: `manifest.webmanifest` + `sw.js` + install flow + Web Push
- Integrations:
- Kavenegar OTP (`verify/lookup`)
- Kavenegar SMS send + status APIs
- Email sending for orders/contact/agency forms

## 3) Roles and Access Model

| Role | Main Access |
|---|---|
| Guest | Browse catalog, product search, contact/agency forms, local cart |
| Customer | Profile, own orders, own files, push opt-in, profile edit |
| Marketer (Sales Consultant) | Dashboard, scan-to-cart, add customer, upload files to own customers, view invoices |
| Accountant | Dashboard, invoice management, status/sepidar updates, delete invoice, inventory upload, product trace, customer file operations |
| Admin | Full access: user creation, customer management with ranking, analytics, allocation tool, push/SMS center, logs, online users |

## 4) Full Functional Scope (Feature-by-Feature)

### 4.1 Catalog and Discovery

- Brand list from `brands.json` with real product counts.
- Brand pages with:
- Pagination/infinite load
- In-brand search
- Sort modes (`new`, `price_asc`, `price_desc`)
- Stock-first ordering (in-stock and backorder shown first)
- Global search and in-category search across:
- Product title
- SKU
- Reference attribute
- Order-code attribute (`custom order-code attribute slug`)
- Product cards include:
- Thumbnail
- Title
- Price (from app price table)
- Order code
- Stock status
- Persistent visual highlight when product is in cart.

### 4.2 Product Page and Media UX

- Product detail fields:
- Title
- Featured image
- Price
- Reference
- Case size
- Order code
- Dynamic stock quantities
- Reserved quantities (privileged roles)
- Full gallery modal with:
- Tap-to-open
- Pinch zoom
- Lens magnifier
- Pan and double-tap zoom handling
- Proper frame clipping so zoom does not overflow container
- Share button:
- Native share sheet where available
- Fallback copy-link flow
- Back navigation persistence:
- Returns user to exact previous product position inside category/search lists
- Sticky header with search on listing pages.

### 4.3 Cart and Checkout

- Sticky cart behavior with always-visible totals.
- Cart row content includes image, order code, price, quantity controls.
- Out-of-stock products block add-to-cart.
- Customer data form supports:
- Auto-fill by mobile lookup (`customer_lookup`)
- Role-aware required fields
- Mandatory sales consultant link for customer records
- Marketer workflow:
- Cart view remains accessible
- Customer form is enforced during finalization flow
- Duplicate-product guard in unfinalized cart:
- If same product/order-code is added again, marketer gets a confirmation prompt
- User can add incremental quantity or cancel (no duplicate row is silently added)
- Order submission:
- Validates payload and pricing table mapping by order code
- Stores customer snapshot
- Stores item-level details including brand/order code/title
- Generates order number sequence:
- Starts at `100`
- Increments by step `2` (`100, 102, 104, ...`)
- Sends order email with attached CSV snapshot.

### 4.4 Profile Experience

- Customer profile:
- Basic account data
- Edit profile (mobile immutable in UI where required by role policy)
- Orders list with status and totals
- Order export download (`.xlsx`)
- Customer files panel with downloads
- Marketer/Admin/Accountant profile areas:
- Role and account identity shown in Persian labels
- Logout actions in dashboard/profile flows
- Push activation toggle.

### 4.5 Dashboards and Analytics

- Jalali date filtering across dashboards.
- Quick range presets:
- 30 days
- 14 days
- 7 days
- Yesterday
- Start of current Jalali year
- Default range behavior:
- Current Jalali month start to current day
- KPI cards:
- Order count
- Revenue
- Sold items
- New customers
- Total customers
- Total consultants (admin scope)
- Admin analytics extras:
- Top 10 brands table (sortable)
- Top 10 best-selling references/products
- Brand filter for top products
- Product thumbnail link to product page
- Marketer ranking panel by revenue.

### 4.6 Invoice Management and Accounting

- Full invoice edit modal (admin/accountant): update customer, add/remove products, edit quantities.
- Transactional save recalculates totals and customer ownership to avoid stale attribution when an invoice moves to another customer.
- Item prices are re-evaluated server-side from order-code pricing on every invoice edit save.
- Reservation rows are rebuilt on invoice edits to preserve inventory allocation integrity.

- Managed invoice table with:
- Order number
- Sepidar invoice number
- Sepidar editor (inline pencil action)
- Registrar metadata (who/when set Sepidar number)
- Customer
- Consultant
- Item count
- Brand list in order
- Status dropdown
- Last status update timestamp and actor
- Amount
- Excel export action
- Delete action with two-step confirmation
- Order status workflow:
- `preinvoice` (with backward compatibility for `submitted/draft`)
- `invoiced`
- `awaiting_doc`
- `accounting_approved`
- `post_delivered`
- `canceled`
- Status change log table with actor and timestamp.
- Inventory side-effects:
- Cancel releases reserved unique codes
- Invoiced + Sepidar-ready can consume reserved allocations.

### 4.7 Inventory, Barcode, and Reservation Engine

- Inventory source is **unique-code table** (not only Woo stock field).
- Inventory upload supports CSV/XLSX:
- Column A: order code
- Column B: unique product code (barcode unique id)
- Optional column C: price in Rial (toggle `include_price`)
- Upload processing:
- Upsert active unique codes
- Deactivate missing unique codes
- Update app price table by order code
- Sync Woo stock metadata and optional prices
- Mark products out-of-stock when no active code remains
- Produce downloadable “missing products” CSV report when order code exists in file but no product mapping is found
- Scanner flow:
- Fixed floating scan button in catalog/brand contexts
- Uses `BarcodeDetector` when available
- Falls back to ZXing when needed
- Scanned unique code resolves to order code and product
- Auto-add behavior with reservation checks
- Reservation fallback policy:
- If the sampled/scanned unique code is unavailable, mismatched, or already assigned, the system attempts to reserve the first available unique code from the same order code.
- Only when no allocatable unique code remains, the line is stored as warning-based/manual-without-code.
- Handles already-assigned, mismatch, and shortage scenarios
- Supports manual-without-code allocation when fully reserved and user confirms
- Product trace tool (admin/accountant/marketer):
- Input unique code
- Shows whether in stock, reserved, or invoiced
- Shows linked invoice/customer/order data when consumed.

### 4.8 Allocation Tool (Admin)

- Dedicated “Allocate” modal with independent Jalali date range.
- Rank filter (A/B/C/D/E).
- Detects oversold references by comparing ordered qty to available inventory.
- Prioritizes customers by selected ranks and order time.
- Produces allocation table:
- Ordered qty
- Allocated qty
- Remaining/shortage per reference.

### 4.9 File Distribution to Customers

- Admin/Accountant/Marketer can upload files to customer profiles.
- Marketer is restricted to own customers.
- File panel includes:
- Searchable customer selector
- Upload form
- File table with Jalali date, customer, uploader, download, delete
- Customer sees assigned files in own profile and can download.

### 4.10 Communications: Push and SMS

- Web Push:
- Public key endpoint
- Subscription/unsubscription
- Notification inbox fetch for SW
- Unread/read tracking per user identity tuple
- Admin push panel:
- Role-based targeting
- Recipient search
- Customer rank filtering
- Send to single recipient or all in role/rank scope
- Automatic push events:
- Order status change -> customer + related marketer
- New customer file upload -> customer
- SMS:
- OTP request and verify via Kavenegar template lookup
- Admin SMS panel:
- Role/rank targeting
- Searchable recipient list
- Send single/all
- SMS logs include:
- Recipient
- Message
- Message ID
- Delivery status code/text
- Status refresh from Kavenegar `sms/status`.

### 4.11 Admin Governance Tools

- Add user modal with role selection:
- Marketer
- Accountant
- Admin
- Customer (through dedicated customer-creation flow)
- Admin customer management modal:
- Search and select customer
- Edit profile fields
- Set customer rank (`A`..`E`)
- View customer purchase summary:
- Order count
- Purchased brands
- Total volume
- User activity logs modal with Jalali date filter
- Online users modal with live refresh.

### 4.12 Contact and Agency Forms

- “Contact Us” form:
- Full validation
- Rate limit
- Sends email to configured inbox
- “Agency Request” form:
- Full validation
- File upload (shop sign image)
- Rate limit
- Sends multipart email with attachment
- Contact section supports clickable phone/email links and map actions.

### 4.13 PWA, Session, and Client Behavior

- Install prompt and iOS-specific add-to-home guidance.
- Standalone mode support (`display: standalone`).
- Service worker cache versioning (`BUILD`), safe update activation.
- Navigation fallback for offline shell.
- Static asset cache normalization to avoid duplicate cache entries.
- Keep-login behavior with remember cookie + server session restore.
- Logout only on explicit action (as configured by auth/session policy).

### 4.14 Observability and Error Handling

- Global server error handlers for fatal/exception warnings.
- Structured API error responses with `error_id` on server failures.
- Client error logger endpoint for JS/API failures.
- Business activity logs (`user_activity_logs`) with Persian message lines.
- Live user session tracking (`user_sessions`).

## 5) Data Model Coverage

Main operational entities (created by migrations):

- `users`
- `marketers`
- `customers`
- `orders`
- `order_items`
- `order_status_logs`
- `customer_files`
- `inventory_unique_codes`
- `order_item_unique_allocations`
- `inventory_upload_logs`
- `order_code_prices`
- `push_subscriptions`
- `notifications`
- `notification_reads`
- `sms_logs`
- `user_activity_logs`
- `user_sessions`
- `otp_codes`

Migrations are under `migrations/001_init.sql` to `migrations/013_order_code_prices.sql`.

## 6) Complete API Surface (Public-Safe Inventory)

### 6.1 Catalog and Public Form APIs (`/api`)

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/brands.php` | GET | Public | Brand list and product counts |
| `api/products.php` | GET | Public | Brand products, in-brand search/sort, stock/price enrichment |
| `api/product.php` | GET | Public | Single product detail with stock/reserved summary |
| `api/gallery.php` | GET | Public | Product gallery image list |
| `api/search.php` | GET | Public | Global product search |
| `api/submit_order.php` | POST | Public/Auth-aware | Create order, reserve unique codes, email + template SMS hooks |
| `api/submit_contact.php` | POST | Public | Contact form email |
| `api/submit_agency.php` | POST | Public | Agency request form with attachment |

### 6.2 Authentication and Session (`/api/v2`)

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/auth_request.php` | POST | Public | Request OTP (Kavenegar verify/lookup) |
| `api/v2/auth_verify.php` | POST | Public | Verify OTP, create session, set role |
| `api/v2/auth_admin_hint.php` | POST | Public | Check whether admin password login is available for mobile |
| `api/v2/auth_password.php` | POST | Public (admin mobile only) | Password-based admin login |
| `api/v2/me.php` | GET | Session | Session identity + role + profile + password change flag |
| `api/v2/password_change.php` | POST | Admin | Change admin password / clear first-login flag |
| `api/v2/logout.php` | POST | Session | Logout + remember-cookie clear |

### 6.3 Profile and Customer Self-Service

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/profile_update.php` | POST | Guest/Customer/Marketer/Admin-with-marketer | Update allowed profile fields |
| `api/v2/customer_lookup.php` | GET | Public | Auto-fill customer info by mobile |
| `api/v2/customer_orders.php` | GET | Customer/guest mobile | List own orders |
| `api/v2/customer_files.php` | GET | Customer/guest mobile | List own files |
| `api/v2/file_download.php` | GET | Role-aware | Secure file download authorization |

### 6.4 Dashboard and Reporting

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/dashboard_summary.php` | GET | Admin/Marketer | KPI cards, recent orders, top marketers |
| `api/v2/dashboard_admin_extras.php` | GET | Admin | Top brands and top products datasets |
| `api/v2/dashboard_marketers.php` | GET | Admin | Marketer performance list |
| `api/v2/dashboard_orders.php` | GET | Privileged | Legacy paged order list/filter |
| `api/v2/dashboard_stats.php` | GET | Privileged | Legacy aggregate stats |
| `api/v2/accountant_orders.php` | GET | Admin/Accountant/Marketer | Managed invoice table data + totals |

### 6.5 Orders and Invoice Operations

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/order_status_update.php` | POST | Admin/Accountant | Update status, log, notifications, inventory side-effects |
| `api/v2/order_sepidar_update.php` | POST | Admin/Accountant | Set/edit Sepidar number and trigger inventory consume check |
| `api/v2/order_delete.php` | POST | Admin/Accountant | Delete order |
| `api/v2/order_export.php` | GET | Role-aware | Generate downloadable `.xlsx` order file (with image embedding and unique codes) |

### 6.6 Customer/User Management

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/customer_create.php` | POST | Admin/Accountant/Marketer | Create/update customer and attach consultant |
| `api/v2/customers_list.php` | GET | Admin/Accountant/Marketer | Search/list customers (marketer-scoped when needed) |
| `api/v2/admin_customer_get.php` | GET | Admin | Customer detail + purchase stats |
| `api/v2/admin_customer_update.php` | POST | Admin | Update customer fields + rank |
| `api/v2/user_create.php` | POST | Admin | Create marketer/admin/accountant users |
| `api/v2/marketer_create.php` | POST | Admin | Legacy marketer creation endpoint |
| `api/v2/marketers_public.php` | GET | Public | Active consultant list for selectors |

### 6.7 Inventory, Scanner, Allocation

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/inventory_upload.php` | POST | Admin/Accountant | Upload unique-code stock and optional prices, sync Woo |
| `api/v2/inventory_scan_lookup.php` | GET | Admin/Accountant/Marketer | Resolve scanned unique code to product/inventory state |
| `api/v2/product_trace.php` | GET | Admin/Accountant/Marketer | Trace unique code to invoice/product status |
| `api/v2/allocate_tool.php` | POST | Admin | Rank-based oversold allocation analysis |

### 6.8 File Management (Operational)

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/accountant_upload.php` | POST | Admin/Accountant/Marketer | Upload file for customer |
| `api/v2/accountant_files.php` | GET | Admin/Accountant/Marketer | List operational file records |
| `api/v2/accountant_file_delete.php` | POST | Admin/Accountant/Marketer (scoped) | Delete uploaded file |

### 6.9 Push Notifications

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/push_public_key.php` | GET | Public | VAPID public key |
| `api/v2/push_subscribe.php` | POST | Auth | Store/activate push subscription |
| `api/v2/push_unsubscribe.php` | POST | Auth | Deactivate push subscription |
| `api/v2/push_inbox.php` | POST | SW endpoint-based | Pull unread notifications for push event |
| `api/v2/notifications_unread.php` | GET | Auth | In-app unread notifications |
| `api/v2/notifications_mark_read.php` | POST | Auth | Mark notifications as read |
| `api/v2/push_send.php` | POST | Admin | Targeted push send by role/rank/recipient |

### 6.10 SMS Operations

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/recipients_list.php` | GET | Admin/Marketer | Recipient listing by role with search/rank |
| `api/v2/sms_send.php` | POST | Admin | Bulk/single SMS send via Kavenegar |
| `api/v2/sms_logs.php` | GET | Admin | SMS history with message ID/status |
| `api/v2/sms_status_refresh.php` | POST | Admin | Refresh delivery status from Kavenegar |

### 6.11 Observability and Health

| Path | Method | Access | Purpose |
|---|---|---|---|
| `api/v2/log_client_error.php` | POST | Public | Store client-side errors in server logs |
| `api/v2/user_logs.php` | GET | Admin | User activity log feed |
| `api/v2/online_users.php` | GET | Admin | Active session users |
| `api/v2/ping.php` | GET | Public | App DB health check |

## 7) Security Controls Implemented

- Same-origin enforcement for state-changing endpoints.
- HTTP method guard per endpoint.
- Role guard per endpoint.
- Input normalization/validation for mobile, ids, dates, enums.
- Rate limiting on sensitive/public forms (`otp`, `contact`, `agency`).
- Security headers:
- `X-Content-Type-Options`
- `X-Frame-Options`
- `Referrer-Policy`
- `Permissions-Policy`
- Optional HSTS over HTTPS
- Secure session and remember-cookie options:
- `HttpOnly`, `SameSite=Lax`, secure cookie on HTTPS
- Structured server error logging with correlation IDs.

## 8) Performance and Reliability

- JSON cache for stable catalog endpoints with ETag support.
- Frontend GET caching layer for fast route transitions.
- Lazy image loading and bounded list rendering.
- Service worker:
- Versioned cache
- Safe activation
- Navigation fallback
- Static cache normalization
- Scanner pipeline optimized with native detector + fallback strategy.

## 9) Configuration (Non-Secret Key Map)

Set these in `config.php` (copy from `config.sample.php`):

- DB and app DB:
- `DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASS`, `WP_PREFIX`
- `JT_APP_DB_HOST`, `JT_APP_DB_NAME`, `JT_APP_DB_USER`, `JT_APP_DB_PASS`
- App/session:
- `JT_APP_SECRET`, `JT_SESSION_COOKIE`, `JT_SESSION_TTL`
- Optional remember: `JT_REMEMBER_COOKIE`, `JT_REMEMBER_TTL`
- UI/assets:
- `JT_ASSET_VER`, `SITE_TITLE`, `SITE_BRAND`, `ITEMS_PER_PAGE`
- Email:
- `ORDER_TO_EMAIL`, `ORDER_FROM_EMAIL`, `ORDER_FROM_NAME`
- SMS/Kavenegar:
- `JT_KAVENEGAR_API_KEY`, `JT_KAVENEGAR_TEMPLATE`, `JT_KAVENEGAR_SENDER`
- Push/VAPID:
- `JT_VAPID_PUBLIC_KEY`, `JT_VAPID_PRIVATE_KEY_B64`, `JT_VAPID_SUBJECT`

## 10) Setup and Run

1. Copy `config.sample.php` to `config.php` and fill values.
2. Ensure DB schema is up-to-date by running migration files in `migrations/`.
3. Ensure PHP extensions required by enabled features are available:
- `pdo_mysql`, `mbstring`, `curl`, `openssl`, `zip`, `dom`, `gd`
4. Deploy with web root on project folder and serve `index.php`.
5. Validate:
- `api/v2/ping.php`
- login (OTP)
- dashboard access by role
- inventory upload
- push/SMS test paths.

## 11) Repository Safety Notes

- Keep `config.php` and any environment-secret files out of public commits.
- Do not commit runtime logs, SQL dumps with production data, or private keys.
- This README is intentionally exhaustive on functionality and intentionally silent on secrets.

## 12) Latest Update Notes

### v2026.2.44

- Fixed add-to-order button click detection when event target is a text node in some browsers.
- Added robust event-target normalization for:
- global add button delegation (`[data-additem]`)
- brand card click/pointer handlers (to avoid accidental miss/override)
- Bumped cache-bust version (`JT_ASSET_VER`, `index.php`, `sw.js`, `manifest`).

### v2026.2.43

- Fixed quantity-modal add flow to avoid hidden duplicate-prompt blockers.
- For marketer duplicate items inside quantity modal:
- The modal now shows duplicate notice with current count.
- Entered quantity is applied directly as incremental quantity on confirm.
- Added cache-bust version bump (`JT_ASSET_VER`, `index.php`, `sw.js`, `manifest`).

### v2026.2.42

- Fixed add-to-order issue from quantity modal on some browsers/webviews.
- Duplicate-item flow for marketers is now resilient when browser `prompt` is blocked.
- Added fallback confirmation path so add action does not silently fail.
- Bumped deploy cache versions (`JT_ASSET_VER`, `index.php`, `sw.js`, `manifest`).

### v2026.2.41

- Inventory visibility rule adjusted:
- Product availability no longer decreases at reservation time.
- Visible stock now decreases only by consumed (finalized) allocations.
- Consumption trigger adjusted:
- Reserved unique codes are consumed only after a Sepidar invoice number is set.
- Status-only changes no longer consume inventory without Sepidar number.

### v2026.2.40

- Enabled product trace access for `Marketer` role in dashboard and API policy.
- Added marketer duplicate-add guard in unfinalized cart:
- Re-adding the same product triggers quantity-increment confirmation.
- Cancel action now safely aborts duplicate add.
- Added customer quick-select in finalize-order customer modal for:
- `Admin`
- `Accountant`
- `Marketer`
- Selecting a customer auto-fills the full customer form.
