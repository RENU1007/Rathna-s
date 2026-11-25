# Rathna's Cakes & Bakes - Firebase Setup

## Files
- `index.html`: complete GitHub Pages app
- `firestore.rules`: security rules

## 1. Create Firebase project
1. Open https://console.firebase.google.com/
2. Add project: `rathna-bakery`
3. You may disable Google Analytics.

## 2. Create Firestore
1. Firebase Console > Build > Firestore Database > Create database.
2. Choose Standard edition.
3. Choose a nearby region. For Chennai, select an India region offered by the console.
4. Start in Production mode.

## 3. Enable login
1. Build > Authentication > Get started.
2. Sign-in method > Email/Password > Enable.
3. Authentication > Users > Add user.
4. Create exactly five staff accounts. Do not add a public Sign Up page.

## 4. Register the web app
1. Project settings (gear icon) > General > Your apps > Web (`</>`).
2. Name it `rathna-bakery-web`; Firebase Hosting is not required.
3. Copy the `firebaseConfig` values.
4. Open `index.html` and replace all `PASTE_...` placeholders.

## 5. Publish Firestore rules
1. Firestore Database > Rules.
2. Replace the editor with the contents of `firestore.rules`.
3. Click Publish.

The rules allow only authenticated staff. Bills and transactions are append-only from the browser. Products and shops can be managed by any signed-in staff member in this first version.

## 6. Deploy on GitHub Pages
1. Create/copy these files into your existing repository root.
2. Commit and push.
3. Repository > Settings > Pages.
4. Source: Deploy from a branch.
5. Branch: `main`, folder `/ (root)`, then Save.
6. Wait a few minutes and open the Pages URL.

## 7. Firebase authorized domain
In Firebase Console > Authentication > Settings > Authorized domains, add only the host name, for example:
`YOUR-USERNAME.github.io`

If you use a custom domain later, add that domain too.

## 8. First test
1. Sign in with one staff account.
2. Add 2 products.
3. Add 1 shop.
4. Create a test bill and save it.
5. Add a petrol expense.
6. Check the monthly report.
7. On Firestore Database > Data, confirm `products`, `clients`, `bills`, and `transactions` exist.

## Important accounting behavior
- A saved bill uses a Firestore transaction to update the shop pending balance safely.
- `billAmount` records sales. `received` records cash collected in the bill document.
- The current simple profit report calculates Income - Expense. For accounting-grade profit, add cost-of-goods/product cost later.
- Do not delete a shop that already has bills. A production version should use `active: false` instead.

## Security notes
- Firebase web config is expected to be visible in browser code. Security comes from Authentication and Firestore Rules.
- Never add a service-account JSON/private key to GitHub.
- Keep the repository free of private customer notes beyond what the app stores in Firestore.
