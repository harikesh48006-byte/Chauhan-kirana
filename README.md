# Chauhan Kirana Store — GitHub + Google Sheets

## Files
- `index.html`: Website, cart, WhatsApp order, admin panel (PIN 1207), product CRUD, image upload.
- `Code.gs`: Google Apps Script backend for Google Sheets and Drive image uploads.

## A. Google Sheet backend setup
1. Create/open the Google Sheet you want to use.
2. From the Sheet, select **Extensions → Apps Script**.
3. Replace the editor contents with `Code.gs` from this folder and save.
4. In Apps Script, open **Project Settings → Script Properties** and add:
   - Property: `ADMIN_PIN`
   - Value: `1207`
5. Select `setup` from the function dropdown and click Run. Approve the requested Google permissions.
6. Click **Deploy → New deployment → Web app**.
   - Execute as: **Me**
   - Who has access: **Anyone**
   Deploy and copy the URL ending in `/exec`.
7. Keep the deployment URL private enough to avoid casual abuse. Server mutations require the PIN, but a public endpoint can still be targeted; use a strong PIN and rotate it in Script Properties when needed.

## B. Configure website
Open `index.html` and replace:
- `PASTE_YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE` with your deployed `/exec` URL.
- `REPLACE_WITH_10_DIGIT_WHATSAPP_NUMBER` with the shop's WhatsApp number (10 digits, no +91).

Commit both files to the same GitHub repository. For GitHub Pages, publish from the branch/folder containing `index.html`.

## C. Admin
Click **दुकानदार** and use PIN `1207`. Add/edit/delete products. Product photos can be uploaded (max 1.5 MB) to Google Drive; the resulting image URL is saved to the Sheet.

## D. Important notes
- Google Apps Script deployment is required. Without it, the site intentionally shows "Setup needed"; local demo changes do not sync to Google Sheets.
- `Products` sheet columns are created by `setup`: `id, name, price, stock, category, imageUrl, updatedAt`.
- Customer orders open WhatsApp; they are not automatically written to the Sheet.
- `Anyone` access makes the API reachable publicly. The backend checks PIN for write operations, but this is a starter setup, not a hardened commerce backend. Avoid storing sensitive customer data in this static site.
- This starter includes product management and kirana ordering. It does not include the original tent-house booking workflow.
