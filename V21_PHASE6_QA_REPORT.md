# V21 Phase 6 — Static QA Report

## Static checks
- PASS — Backend Js Syntax
- PASS — Frontend Inline Js Syntax
- PASS — Family Login Backend
- PASS — Family Permission Backend
- PASS — Inventory Backend
- PASS — Order Stock Deduction Backend
- PASS — Fifo Batch Backend
- PASS — Verified Purchase Reviews
- PASS — Review Moderation Backend
- PASS — Sales Dashboard Backend
- PASS — Product Description Backend
- PASS — Product Description Frontend
- PASS — Whatsapp Business Api Absent

## Important limitations — integration testing still required
- These checks validate JavaScript syntax and presence of key implementation paths only. They do not execute Google Apps Script services or connect to Firebase / Google Sheets.
- Do not deploy this package to the live spreadsheet/site yet.
- Run the first integration pass against a COPY of the spreadsheet and a test Apps Script deployment.
- Verify stock units carefully (e.g. piece, kg, litre) against the quantity units stored in product records before enabling automatic deductions.
- Test an order with mixed tracked batches and legacy unbatched stock; confirm FIFO batch balances and total product stock reconcile after Confirmed and Cancelled transitions.
- Test duplicate status submissions, concurrent order confirmations, cancellation after delivery, and order edits. Ensure stock is never deducted/restored twice.
- Test that family users cannot call owner-only account-management functions and cannot use permissions they were not granted.
- Confirm every admin/family frontend action uses the session token and server-side permission gate.
- Confirm expiry alert date/time behaviour and stock threshold (currently the UI/backend uses a fixed low-stock threshold of 5).
- Confirm Firebase OTP flows using a real test phone number and Firebase test configuration.
- Verify rating eligibility with a delivered order and ensure only approved reviews affect public averages.
- Verify order totals and item prices are recalculated/validated server-side, including loose/manual items and delivery fees.
- Verify category image uploads, customer order ownership, profile-photo uploads, Tent House independence and 2 km Kirana-only restriction.
- WhatsApp Business API is intentionally out of scope. Existing manual WhatsApp sharing should be regression-tested only.

## Deployment safety
- V20 source and live website have not been changed by this QA pass.
- This V21 copy is not approved for production deployment until the integration tests above pass.
