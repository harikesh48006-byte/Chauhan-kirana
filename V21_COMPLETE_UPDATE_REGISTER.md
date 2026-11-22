# Chauhan Kirana Store — V21 COMPLETE UPDATE REGISTER

This register consolidates the previously discussed requirements so that no agreed point is silently dropped.
WhatsApp Business / WhatsApp Business API integration is EXCLUDED from V21 as explicitly requested.
Normal existing WhatsApp share behaviour may be preserved, but do not add API automation or migrate/connect the shop's number.

## A. Non-negotiable project rules
- Treat the uploaded V20 `index.html` and `Code.gs` as the source of truth.
- Keep V20 untouched; V21 is a separate working copy.
- Preserve the existing look, layout, colours, content, working features and customer experience unless a specific change below requires an addition.
- Preserve the existing Google Spreadsheet ID, Apps Script Web App URL, Firebase project/configuration and existing customer/order data.
- Do not clear, recreate, overwrite or migrate existing customer, product, category, order, ratings or tent data.
- Add new sheet structures/columns additively and make migrations safe/idempotent.
- The 2 km service-radius restriction applies only to Chauhan Kirana Store, never Ram Lakhan Tent House.
- Do not deploy to the live website or live Apps Script until the separate V21 copy has been tested and the user explicitly approves deployment.
- No separate delivery-boy website/panel. Delivery is handled by the owner/admin and family members through the admin system.
- No WhatsApp Business/API work in this version.

## B. Customer entry, account and profile
1. First screen must be the Chauhan Kirana Store login/registration screen; after successful login/registration, open the store page.
2. Keep the existing branded login/register design and store introduction.
3. Customer login/registration uses mobile number and customer name, with account PIN/password support as already designed.
4. Firebase Phone Authentication OTP:
   - OTP-based login/verification.
   - Forgot PIN/password via OTP sent to the registered mobile.
   - Verify OTP before sensitive account recovery / authentication actions.
   - Do not reintroduce MSG91; Firebase Phone Auth is the selected direction.
5. Customer profile:
   - View and edit profile details.
   - Upload/change profile photo.
   - Change PIN/password only after verifying old PIN/password (or secure OTP recovery).
6. Customer order history and order status/tracking.
7. Customer favourites / wishlist.
8. Customer must only see their own profile, favourites and orders.

## C. Storefront, products, categories and cart
1. Preserve existing product listing, search, voice search, categories, cart and checkout.
2. Category/collection image management:
   - Admin can upload/change category image.
   - Customer sees category photo and category name on category cards.
   - Support collections such as Daily Items, Puja Items, Diwali Special and Festival Special.
3. Product details, images, pricing, units and availability should remain consistent between customer and admin views.
4. Loose Items / Khula Saman:
   - Customer can add an open/loose item by entering a rupee budget (example: ₹50 open oil).
   - Admin defines the rate per unit.
   - System calculates quantity/amount from the rupee value and rate.
   - Every add action creates a separate cart line; same loose item can be added multiple times.
   - Also support manual loose item entry with item name and rupee value where configured by the shop.
5. Product ratings and reviews:
   - 1–5 star rating and optional short review.
   - Show average rating and review count on product cards/details.
   - Prefer/require verified-purchase eligibility: only customers who purchased the product can review.
   - Admin moderation controls to approve/hide/delete reviews.
   - Do not trust a typed mobile number as proof of purchase; bind review to authenticated customer/order records.
6. Customer-facing stock display must not expose internal exact stock counts unless explicitly configured; show availability/out-of-stock state instead.

## D. Delivery radius and checkout
1. Kirana customer service restricted to within 2 km of the shop.
2. Enforce the distance rule on the server during order submission, not only in browser UI.
3. Explain clearly to customers outside the service radius that delivery is unavailable.
4. Do not apply this 2 km restriction to Ram Lakhan Tent House.
5. Preserve the existing checkout and order confirmation flow.

## E. Admin / Owner dashboard — one panel, no delivery-boy panel
1. Secure Admin/Owner login separate from customer login.
2. Admin controls and edit actions must be hidden from ordinary customers AND protected on the backend.
3. Dashboard overview:
   - Today's sales and orders.
   - Date-filtered sales.
   - Order counts and status summaries.
   - Recent orders and useful business metrics.
4. Order management:
   - View new, active, completed and cancelled orders.
   - Accept/confirm or reject/cancel orders.
   - View full order details and customer contact/delivery details.
   - Update order status.
   - Correct/edit order items and quantities where permitted; recalculate totals safely and retain an audit trail.
   - Print/download/share customer bill using the existing supported flow.
   - Search/filter by order number, customer, date and status.
5. Status lifecycle should support the practical family workflow, for example:
   New/Pending → Confirmed → Processing → Packed → Out for Delivery → Delivered; plus Cancelled.
   Keep statuses consistent across admin, customer order history and notifications/UI.
6. Family-managed delivery:
   - No separate delivery-boy panel/site.
   - Owner/admin can record which family member is handling/delivering an order.
   - Family members with permission can update assigned order status from the same admin system.
   - Record who changed status and when.
7. Customer management:
   - Find/view customer details and order history.
   - Do not expose one customer's private details to another customer.
8. Admin settings and audit:
   - Securely change owner/admin credentials.
   - Record important changes (order edits, stock adjustments, status changes, user/role changes).

## F. Family access and permissions
1. Owner account has full control.
2. Owner can create, disable and manage family-member accounts.
3. Each family member has an individual login; do not share one common owner PIN for everyone.
4. Role/permission options should be configurable, with sensible permissions such as:
   - Orders/status: view and update orders.
   - Inventory: stock in/out and product stock management.
   - Products/categories: edit product details, prices and category images.
   - Reports: view sales reports.
   - Owner-only: manage accounts, roles, security settings and sensitive configuration.
5. Enforce permissions in backend endpoints, not merely by hiding buttons in HTML.
6. Track who performed important actions and timestamps.
7. Owner can revoke a family member's access.

## G. Inventory, stock and expiry
1. Product stock opening balance / current stock.
2. Stock In: purchases/restocking with quantity, date, source/supplier and optional cost.
3. Stock Out: sales/order deduction and manual adjustment with reason.
4. Stock ledger/history: every stock movement with before/after quantity, timestamp and responsible account.
5. Automatically deduct stock when the order reaches the agreed fulfilment point; avoid double deduction if status is retried or edited.
6. Restore stock safely for cancelled orders/returns, without double restoration.
7. Low-stock threshold per product and low-stock alerts in admin.
8. Expiry tracking by batch/lot where needed:
   - Product/batch expiry date and quantity.
   - Upcoming expiry alerts.
   - Expired stock warning and ability to mark/remove expired quantity.
9. Stock adjustment must be permission-controlled and auditable.
10. Do not let a customer manipulate price, quantity, discount or total by editing browser data; backend recalculates from trusted product/rate data.

## H. Sales reports and business records
1. Daily, weekly, monthly and custom date-range reports.
2. Total orders, delivered orders, cancelled orders and pending orders.
3. Gross sales/order totals with clear treatment of cancelled orders and discounts.
4. Product-wise sales and quantity.
5. Stock movement / restocking reports.
6. Export/print capability where practical.
7. Reports must use consistent date/time and order-status rules.
8. Existing basic V20 dashboard/report functions should be extended, not removed.

## I. Bills, WhatsApp share and existing usability fixes
1. Preserve existing manual WhatsApp bill/order sharing only; NO WhatsApp Business API integration or automated API messaging in V21.
2. Ensure quantities display as whole-number units such as “1 Piece” instead of “1.000” in printed bills and WhatsApp order text where the unit is whole-number based.
3. Fix WhatsApp order/share button alignment so it stays within the page and does not shift sideways.
4. Keep bill totals, discounts, loose-item calculations and order totals consistent across cart, saved order, print view and WhatsApp share text.
5. Preserve the existing customer bill sharing workflow; do not require a printer.

## J. Ram Lakhan Tent House
1. Preserve the separate Tent House section/pages and existing booking functionality.
2. Preserve tent items, gallery and video/photo content functionality already present.
3. Keep Tent House independent from Kirana inventory and 2 km service-radius restrictions.
4. Do not let Kirana-only changes break Tent House pages or booking data.

## K. Security, reliability and testing
1. Review all public and write API actions.
2. Use authenticated sessions with expiry and role checks for admin/family operations.
3. Never rely on frontend-only permission checks.
4. Validate order ownership, product IDs, quantities, rates, totals, stock changes and status transitions server-side.
5. Add safe error handling, duplicate-request protection and audit logs.
6. Do not expose admin PINs, customer PINs, Firebase secrets or private data in frontend/source logs.
7. Test registration, OTP login, forgot PIN, profile changes, favourites, cart, loose items, checkout, radius rejection, order status, stock deductions/restoration, family permissions, reports, category uploads, reviews and Tent House separately.
8. Test against a COPY of the Google Sheet and a test Apps Script deployment first.
9. Test mobile and desktop layouts, especially the large existing frontend and WhatsApp share alignment.
10. No live deployment until the complete V21 test pass and explicit user approval.

## L. WhatsApp Business/API explicitly out of scope
- Do not configure WhatsApp Business API, Cloud API, third-party gateways, templates, webhooks or automated messages in V21.
- Do not migrate, disconnect or modify the shop's existing WhatsApp number.
- Revisit only if the user asks in a later version.

## Current source-audit notes (V20)
- V20 already has customer account/profile-related APIs, Firebase OTP-related flows, product/category/tent endpoints, basic ratings, basic admin dashboard/reports and order status functions.
- V20 stock field is not a complete inventory ledger or expiry system.
- V20 admin access is substantially shared-PIN based; family accounts/role-based backend permissions are not yet implemented.
- Existing rating flow must be hardened to authenticated verified-purchase reviews and moderation.
- These are audit observations, not claims that every item above has been implemented.


## V21 implementation progress
- Phase 1 working-copy implementation started: added additive `FamilyUsers` sheet schema, individual family login using salted SHA-256 PIN hashes, owner-only create/list/enable/disable endpoints, permission-aware admin session tokens, and frontend owner/family login plus family account management UI.
- JavaScript syntax checks passed for the current Code.gs and inline frontend scripts.
- This is not yet production-approved: no live spreadsheet migration or deployment has been run. Next phases must implement order screens/actor audit, inventory ledger/expiry, report refinements and remaining feature gaps, followed by full test deployment.


## Additional customer product-view requirement (confirmed during V21 work)
- Customer product cards show a short two-line product description beneath the product name when available.
- Tapping the product name/photo opens the product detail view with a larger product photo, full description, price, availability and Add to Cart action.
- Tapping the detail photo opens the image separately for closer inspection.
- Admin product form includes a Product Description field; backend must save and return this field so it is visible to customers.


## V21 implementation progress — Phase 2 order management
- Added additive order metadata columns: assignedFamilyMobile, assignedFamilyName, statusUpdatedAt, statusUpdatedBy.
- Added an OrderActivityLog sheet (created only when the backend setup/helper path runs; existing order rows are retained).
- Admin order table now includes an optional family-member assignment selector.
- Added Processing to the admin order status choices.
- Status and family assignment changes are logged with actor details from the authenticated admin session.
- These changes are in the separate working copy only. They have not been run against the live Google Sheet or deployed.
- Static JavaScript syntax checks passed for Code.gs and the inline frontend scripts. Apps Script runtime / copied-spreadsheet integration tests remain pending.


## V21 implementation progress — Inventory + motion design
- Added additive `StockLedger` and `ExpiryBatches` sheet helpers; existing Products rows are not rewritten by these helpers.
- Added backend endpoints protected by the `inventory` permission: `adminGetInventory` and `adminRecordStockMovement`.
- Added Stock In, Stock Out and Set Stock controls, optional unit cost/supplier/expiry date/note, movement history, low-stock list (threshold currently 5 units) and expiry alerts (within 30 days).
- Stock In with an expiry date creates a batch record. Expiry batch quantities are tracked separately; automatic batch-level FIFO depletion/expiry stock deduction still requires a later pass and must be tested before live use.
- Added an Inventory & Expiry section to the Admin panel.
- Added subtle CSS motion effects (hover lift, button press, cart pulse, fade-up and shimmer) with `prefers-reduced-motion` support; existing layout and colours are preserved.
- Static JavaScript syntax checks passed for backend and inline frontend scripts. Apps Script runtime, role-permission, spreadsheet-copy integration, mobile layout and stock reconciliation tests remain pending.
- Live website and live Google Sheet remain unchanged.


## V21 implementation progress — Phase 4 customer experience and review moderation
- Customer order items now persist productId for new orders (legacy orders remain unchanged).
- Product reviews now require an authenticated customer session and a matching delivered order item; legacy orders without productId are matched by exact product name.
- New reviews enter Pending status and do not affect public average ratings until approved.
- Owner review moderation endpoints support Approve, Hide and Delete.
- Legacy existing reviews are preserved and treated as Approved; missing review IDs are filled additively so they can be moderated.
- Customer order tracking now includes the Processing step and, where available, the assigned family member name and last status update time.
- Static backend and frontend JavaScript syntax checks passed. Integration tests against a copied spreadsheet remain pending.
- Review verification limitation: old order rows do not contain product IDs; the code uses exact product-name matching for those historical rows. New order rows store product IDs.


## V21 implementation progress — Phase 5 stock reservation / FIFO
- Added idempotent order columns for stock deduction, stock restoration and saved FIFO batch allocations.
- When an order is moved to Confirmed, backend validates product stock and deducts product stock once.
- Expiry batches are consumed by earliest non-expired expiry date first; legacy stock not represented by batches remains in product master stock.
- When a stock-deducted order is Cancelled, saved batch allocations and product stock are restored once.
- Stock ledger entries include orderId references and distinguish ORDER_OUT / ORDER_RESTORE.
- Loose/manual items without productId are not deducted from product stock.
- Runtime, race-condition, and copied-spreadsheet integration tests remain pending; confirm product quantity units match stock units before enabling.


## V21 implementation progress — Phase 5 sales reports
- Added date-filtered report summary: order count, sales excluding cancelled orders, delivered count, cancelled count, pending count and delivered sales.
- Top-selling products are now calculated from the selected date-filtered order set.
- Admin dashboard includes a Download Orders CSV button for the currently loaded filtered order list.
- Backend and frontend JavaScript syntax checks passed.
- Reports are based on order records; inventory valuation, profit/margin and supplier purchase-cost accounting are not yet included.
- Live spreadsheet integration and CSV/browser verification remain pending.


## V21 implementation progress — Phase 6 static QA
- Re-ran Node syntax checks on the complete Code.gs source and all inline frontend JavaScript.
- Checked that key backend/frontend implementation paths exist for family access, inventory, stock deduction/FIFO, verified-purchase reviews, moderation, sales dashboard and product descriptions.
- Static checks do not prove Apps Script runtime or Google Sheets integration; the copied-sheet integration test remains mandatory.
- Do not deploy until the QA report's integration and security tests pass.
