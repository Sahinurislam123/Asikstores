# ASIK STORE — Firebase Grocery Store (GitHub Pages starter)

A responsive Bengali-first grocery storefront with product search/categories, cart, Firebase email/password + Google authentication, Firestore products/orders, Firebase Storage product images, and a small admin panel.

## Important scope notes

- The supplied Firebase Web App config is already entered in `app.js`. Firebase services still need to be enabled and the rules published. If setup is incomplete, Firebase reads/writes may fail; demo products are only starter examples.
- COD order creation is wired to Firestore for testing.
- **Online payment is intentionally not enabled yet.** Do not collect real payments until a secure server-side payment flow is implemented. For Razorpay (or another gateway), the server must create payment orders, verify signatures/webhooks, and only then mark an order paid. Never put a secret key in `app.js` or GitHub Pages.
- The current client-side COD checkout sends the displayed cart totals. For real production use, move order creation and price/stock validation into a trusted Cloud Function/server endpoint. Client-side prices must not be treated as authoritative.
- Replace demo product content, set delivery area/fees, privacy policy, terms, and customer support contact before launch.

## 1. Create Firebase project

1. Open https://console.firebase.google.com/ and select the existing project **asikstore-a91d9**.
2. In Authentication → Sign-in method, enable **Email/Password** and **Google**.
3. In Authentication → Settings → Authorized domains, add your GitHub Pages domain, e.g. `YOUR_GITHUB_USERNAME.github.io` (and your custom domain if used).
4. Create a **Cloud Firestore** database in production mode if it does not exist.
5. Enable **Storage** and confirm the bucket is `asikstore-a91d9.firebasestorage.app`.
6. The Firebase Web App config is already in `app.js`. Never put service-account credentials or private keys in frontend code.

## 2. Set Firebase rules

In Firebase Console → Firestore Database → Rules, paste the contents of `firestore.rules` and Publish.
In Firebase Console → Storage → Rules, paste the contents of `storage.rules` and Publish.

These rules let the public read products, signed-in users create their own COD orders, and only users whose `users/{uid}` document has `role: "admin"` manage products/orders. Test the rules in Firebase Rules Playground before launch.

## 3. Make your account an admin

1. Sign in to ASIK STORE once using your chosen email/Google account.
2. Firebase Console → Authentication → Users → copy your exact UID.
3. Firestore → Data → `users` collection → create document with document ID equal to that UID.
4. Add fields:
   - `role` (string) = `admin`
   - `email` (string) = your email
5. Reload the website. The **Admin Panel** button should appear.

Never let ordinary users edit their own `role`. The supplied rules block role changes from the client; grant admin only through the Firebase Console or a trusted server.

## 4. Test locally

Because `app.js` uses JavaScript modules, open the project through a local web server rather than opening `index.html` as a file. For example, with Python installed:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`. Add `localhost` to Firebase Authentication authorized domains if needed.

## 5. Upload to GitHub Pages

1. Create a GitHub repository, e.g. `asik-store`.
2. Upload `index.html`, `styles.css`, `app.js`, `manifest.json`, `firestore.rules`, `storage.rules`, and `README.md` to the repository root.
3. GitHub → Settings → Pages → Deploy from a branch → select `main` and `/ (root)` → Save.
4. Your URL will be `https://YOUR_GITHUB_USERNAME.github.io/asik-store/` (replace the username and repository name with yours).
5. Add `YOUR_GITHUB_USERNAME.github.io` to Firebase Authorized domains.

## 6. Online payments before launch

To activate online payment, use a trusted backend such as Firebase Cloud Functions or Cloud Run:
1. Backend creates a gateway order using a server-side secret.
2. Frontend opens the gateway checkout using the public key only.
3. Backend verifies the signature and payment webhook.
4. Backend writes verified payment status to Firestore.
5. Firestore rules prevent clients from marking their own order paid.

The current UI deliberately tells users online payment is not active and requires COD. This avoids pretending a payment has succeeded when no payment gateway is connected.

## File map

- `index.html` — page structure
- `styles.css` — responsive storefront styles
- `app.js` — Firebase auth, product list, cart, COD checkout, admin UI
- `firestore.rules` — database access rules
- `storage.rules` — image upload access rules
- `manifest.json` — PWA metadata
