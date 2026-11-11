# Public Update Notes

## 2026-11-12 — Lower homepage presentation

The lower homepage no longer repeats an agency invitation between the brand catalogue and the company videos. Four existing video destinations are grouped into readable cards. The first label now matches its destination, and the agency introduction is shorter and more direct. The existing form uses two columns on desktop and one on mobile. Empty social links are hidden while the footer's working credit and trust links remain.

Live checks at mobile and desktop widths in light and dark preferences confirmed the video and form layouts, price cards, zero horizontal overflow and no JavaScript errors. Brand selection, carousel movement and file selection responded without submitting the form. The shop, product and account entry still loaded after the update. The form submission and authenticated account panel were not exercised.

## 2026-11-12 — Company hero, catalogue prices and account entry

The homepage now introduces JewelTime with its own logo and the slogan «زمان جواهر است», while the Tornado red-car campaign remains in a separate brand feature. Brand carousels show current public catalogue prices, or an inquiry label where no price is available. The shop brand directory, gender links on brand archives, single product presentation and account entry were refined. The old blank login route now opens the existing account form.

Subsequent visual checks led to a complete desktop grid for the ten shop logos, a one-row desktop header and a contained product specifications widget at intermediate widths. These changes use the existing catalogue and commerce controls.

Live checks covered the homepage, shop, Tornado archive, a product and account entry at desktop and mobile widths in light and dark preferences. The product layout was also checked at 1100 px. Prices, page headings, brand links, gallery selection, carousel movement, mobile navigation and password visibility were checked. A transient mobile product layout shift settled without horizontal overflow, and the later intermediate-width specification overflow was fixed and rechecked. Authenticated account pages were not tested, and no purchase, message or login was submitted.

## 2026-11-12 — Official brand campaigns and model browsing

The corporate watch storefront now shows official brand campaign imagery and logos, with Tornado's red-car watch banner on the homepage and its brand page. Selecting a brand reveals its available women's and men's watch models in manual carousels. The presentation uses current public catalogue data, so missing categories do not become invented products. Shop, brand and contact pages also share a cleaner visual treatment.

Live checks covered the homepage, Tornado archive, shop and contact pages at mobile and desktop widths in light and dark browser preferences. The checks confirmed loaded banners, brand selection, both gender rows where present, carousel movement, mobile navigation, search focus, one page heading and no horizontal overflow. No purchase or inquiry was created. Suitable official banners were not verified for every brand, so those tabs continue with logos and available models.

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
