# Chauhan Kirana Store V21 — Upload Guide

## Files
- `index.html` — replace the current frontend file in the GitHub/Firebase Hosting project.
- `Code.gs` — replace the contents of the existing Google Apps Script project's Code.gs.
- `V21_COMPLETE_UPDATE_REGISTER.md` — full agreed feature checklist.
- `V21_UPLOAD_NOTES.md` — this deployment guide.

## Before upload
1. Download a backup of the currently deployed `index.html` and `Code.gs`.
2. Make a copy of the Google Spreadsheet as a backup. V21 backend currently contains the existing production Spreadsheet ID, so its write operations will affect the existing spreadsheet once deployed.
3. Keep the existing Apps Script Web App URL in `index.html`; do not replace it with a guessed URL.
4. In Apps Script > Project Settings > Script Properties, verify `FIREBASE_WEB_API_KEY` exists. Firebase OTP verification depends on it. Do not paste private API keys into public chat.
5. Confirm the Firebase Authentication Phone provider is enabled and the hosted domain is authorized.

## Backend upload
1. Open the existing Apps Script project associated with the current Web App.
2. Open `Code.gs`, replace its contents with the supplied V21 `Code.gs`, and Save.
3. Run `setup()` only if required to authorize/add the additive FamilyUsers structure. Review the execution prompt and confirm the project is the correct one. The setup function also ensures product/category/tent sheets and Drive image folder; it is designed to add missing structures, not clear existing rows.
4. Deploy > Manage deployments > select the existing Web App deployment > Edit.
5. Choose **New version**, keep the existing deployment settings/access, and Deploy.
6. Keep the same Web App URL; the frontend is already configured for the existing URL.

## Frontend upload
1. Replace the repository's current `index.html` with the supplied V21 `index.html`.
2. Commit/push to the existing GitHub repository.
3. If Firebase Hosting is the live host, run the existing Firebase Hosting deploy process from the project folder (do not change Firebase project selection).
4. Open the hosted website in a private/incognito window and hard refresh.

## Important owner/admin PIN behaviour
- Owner PIN logs in as the Owner.
- Legacy `ADMIN_PIN` logs in as a non-owner Admin and cannot manage family accounts.
- Family users sign in with their registered mobile + PIN and only receive their assigned server-side permissions.
- Existing PIN values are read from Apps Script Script Properties. Defaults apply only when properties are absent.

## First things to check after upload
1. Customer login/registration and OTP.
2. Product list, product images, descriptions, category cards and cart.
3. Submit one small test order and check it appears in the admin order list.
4. Change order status and assign a family member.
5. Check stock deduction on Confirmed and restoration on Cancelled.
6. Add one stock-in batch with an expiry date and verify expiry alert.
7. Submit a review for a product in a Delivered order; approve it from Admin.
8. Check reports and CSV export.
9. Check Tent House pages and booking separately.

## Critical caution
This is a V21 upload candidate, not a production-certified release. JavaScript syntax checks pass, but Apps Script runtime, Firebase OTP, spreadsheet schema behaviour, image uploads, stock accounting, and the full UI have not been exercised against the live services. Since the backend has the production Spreadsheet ID in its source, uploading/deploying it will make it operate on the existing live data. Do not deploy until the backup is complete and you accept that risk.

WhatsApp Business API has not been configured or added. Existing manual WhatsApp share code is retained.
