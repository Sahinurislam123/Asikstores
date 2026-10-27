ASIK STORE — Order Details + Category Images update

Replace these two files in your GitHub repository root:
- app.js
- styles.css

Do not replace index.html, firestore.rules, storage.rules, or payment-qr.jpg for this update.

What's changed:
1. Admin Orders now has a clickable “বিস্তারিত দেখুন” button for each order.
2. Order details modal displays customer name, phone, email, full address, delivery note, payment method/status, item list, subtotal, delivery fee, total, and map link/coordinates when saved.
3. Admin can still update order status; “Confirmed / Accept” is available in the status dropdown.
4. Category creation/editing supports an image URL or direct image upload. Uploads go to Firebase Storage under categories/ and the download URL is stored in storeSettings/main categories.
5. Category images display in the storefront category buttons when imageUrl is set; otherwise emoji is shown.

Notes:
- Firebase Storage must be enabled and Storage Rules must permit authenticated Admin uploads to categories/.
- Existing orders without deliveryLocation cannot show a map; only new orders with a selected map location include coordinates.
- Test in a non-production order first. This package was syntax-checked but not tested against the live Firebase project.
