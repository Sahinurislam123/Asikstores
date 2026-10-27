# ASIK STORE — Professional Multi-page Admin

## What changed
- Admin modal now behaves like separate pages: Overview, Website & Branding, Categories, Add Product, Products, Orders.
- Website & Branding edits store name, tagline, logo URL, hero text/image, footer, delivery and contact copy.
- Category Manager supports adding categories, editing category names/icons, and deleting unused categories.
- Categories are saved in Firestore `storeSettings/main` under `categories`.
- Existing product and order management stays in place.

## Update on GitHub Pages
1. Download and extract this ZIP.
2. Replace `app.js` and `styles.css` in the root of your existing `Asikstores` repository.
3. Commit changes to the same branch currently used by GitHub Pages (usually `main`).
4. Wait for Actions to show a green success check, then open the site in Chrome Incognito.

## Firestore requirements
The current `storeSettings/{settingId}` rule must permit Admin create/update. Product create/update/delete and order read/update rules must also permit Admin operations. Do not make rules public just to fix admin access.

Category changes are stored in Firestore. If a category already has products assigned, the admin UI blocks deleting it until those products are moved to another category.
