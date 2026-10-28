ASIK STORE — Cart Product Image Fix 2

This update adds image upload to the existing product edit form. Earlier the cart used a fallback shopping-cart icon when a product had no saved imageUrl.

Install: replace app.js and styles.css in GitHub (styles.css is included unchanged), commit, wait for Pages Success. In Admin > Products, edit each product and either provide a public image URL or upload an image, then Save. The image URL is saved in Firestore and the cart uses it.

Firebase Storage must be enabled and Storage Rules must allow the signed-in Admin to upload. Max upload size: 3 MB. This package has not been tested against the live Firebase project.
