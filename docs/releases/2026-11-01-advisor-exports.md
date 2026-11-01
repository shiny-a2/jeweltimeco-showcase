# Advisor order exports and desktop dialogs

Prepared correction: an advisor recorded on an order can export its spreadsheet after the customer is reassigned. Access remains denied to unrelated advisors. Existing customer and administrative permissions are preserved.

Download controls now show progress and actionable errors instead of silently opening a fallback popup. Spreadsheet signatures are validated before saving. Desktop dialogs are centered with bounded dimensions, and export links have clearer hit areas.

Nine isolated executions of the export endpoint passed, including generated spreadsheet validation and cross-account denial. Eighty-four browser assertions passed with mocked APIs at mobile and desktop widths. Existing ownership, guest-access and service-worker privacy tests passed as well. No customer messages or business records were created. The exact order reported by the user was not identified; live authenticated download confirmation remains pending.

Status: committed and prepared for review; not deployed. Production release requires owner approval.
