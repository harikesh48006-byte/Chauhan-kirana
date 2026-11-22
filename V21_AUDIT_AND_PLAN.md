# Chauhan Kirana Store — V21 Working Copy

IMPORTANT
- This is a separate working copy made from the uploaded V20 source files.
- No live website, Apps Script deployment, Firebase project, or Google Sheet has been changed.
- Keep V20 untouched and retain a separate backup before deployment.
- Existing Spreadsheet ID and Apps Script Web App URL are retained in the copied source.

## Confirmed V21 direction
1. Admin / Owner dashboard
2. Order management and status tracking
3. Family-member access with role-based permissions (no delivery-boy panel)
4. Inventory / stock management and expiry alerts
5. Sales reports
6. WhatsApp Business sharing first; API automation only after provider/configuration decisions

## Initial source audit — findings to address in V21
- The current V20 already contains an Admin Dashboard, date filters, recent orders, customer directory, sales summaries, and basic order-status changes. V21 should extend these rather than replace them.
- The current V20 has a product `stock` field, but no complete stock ledger, stock-in/stock-out history, expiry-lot tracking, or expiry alerts.
- Admin login currently relies on PIN checks and the frontend stores the entered PIN in `adminPin`. Family accounts and role-specific permissions are not implemented.
- Admin dashboard/status endpoints exist, but the current authorization model is shared-PIN based. This needs a proper owner/family account session design before family access is enabled.
- WhatsApp API automation is not configured in the supplied source. Do not connect/migrate the shop's existing WhatsApp number without explicit setup and testing.
- Order status options already include Order initiated, Confirmed, Packed, Out for delivery, Delivered, and Cancelled.
- The existing backend uses the existing Google Spreadsheet ID and Apps Script API URL. Preserve both.

## Safety / implementation rules
- Do not run setup() or deploy code against the live spreadsheet until the migration plan has been reviewed.
- Any new sheet/table must be created additively; never clear or rewrite existing customer/order/product rows.
- Test with a copied spreadsheet and a test Apps Script deployment first.
- Keep Ram Lakhan Tent House independent from the Kirana 2 km delivery-radius rule.
