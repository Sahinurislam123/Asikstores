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
