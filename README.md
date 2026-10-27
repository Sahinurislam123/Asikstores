# ASIK STORE — Compact Green UI Update

This update is based on the existing Firebase/GitHub Pages project and keeps the current Firebase configuration, QR payment image and Firestore/Storage rules.

## UI changes
- Product cards are clickable and open a large detail view with image, price, unit, stock and description.
- Admin can add/edit product descriptions.
- Hero/banner is shorter, especially on mobile.
- Categories are small icon-only buttons in a single horizontal scrolling row.
- Search is a compact icon that expands on click.
- Three-dot header menu includes My Orders, Login/Account and Admin Panel (admin only).
- Local delivery / trust information moved near the bottom, before the footer.

## Publish to GitHub Pages
Replace these files in the root of the existing repository:
- `index.html`
- `styles.css`
- `app.js`

Keep `payment-qr.jpg`, `manifest.json`, `firestore.rules` and `storage.rules` from your current working project. The Firebase Web config remains in `app.js`.

## Important
- Commit the changes and wait for GitHub Pages to deploy, then refresh the site.
- Product descriptions are stored in Firestore as `description`.
- UPI QR payments still require manual confirmation in your bank account before confirming an order. A customer-entered UTR is not proof of payment.


## UPI Intent payment
- Checkout can create a pending order and open a generic `upi://pay` link using the supplied UPI ID `6295979909@sbi`. Verify this UPI ID and payee name in your SBI/UPI app before live use.
- The UPI app may or may not open from every browser. A QR fallback is shown.
- This is **not automatic payment verification**. Orders remain pending until the merchant checks the bank transaction. Never mark an order paid based only on returning to the website or a customer-supplied screenshot/UTR.
- Publish the updated `firestore.rules` if you use `upi_intent`; it allows signed-in customers to create pending COD or UPI-intent orders.
