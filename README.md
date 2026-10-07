# SAMIA’S CLOSET — Firebase ecommerce

A mobile-first React/Vite storefront with Firebase Authentication, Firestore, Storage and callable Cloud Functions.

## What is real here
- Firebase Email/Password + Google authentication.
- Firestore-backed products and authenticated customer cart.
- Firebase Storage product image upload from device gallery/file picker.
- Server-side callable order creation with authoritative Firestore prices, stock validation, transaction-based stock deduction and order image snapshots.
- Firebase custom admin claims and Firestore/Storage rules.
- Customer order history from Firestore.
- Admin product/settings/order views.
- Quiz and weekly-reward callable endpoints with server-side ownership and duplicate-claim checks.

## Important setup
1. Create/confirm Firebase project `sc-new-c05c0`.
2. Enable Authentication: Email/Password and Google.
3. Create Firestore in production mode and Storage.
4. Install Firebase CLI and run `firebase login`.
5. In this folder run `npm install` and `cd functions && npm install`.
6. Run `npm run build` in root and `npm run build` inside `functions`.
7. Deploy: `firebase deploy --only firestore:rules,firestore:indexes,storage,functions,hosting`.
8. The owner must sign in with `rahihumaun369@gmail.com`. The server automatically grants the `admin` custom claim on account creation; `ensureAdminClaim` can be called once for an already-existing owner account after deployment.

## Local development
Create `.env` from `.env.example`, then `npm run dev`.

## Security notes
- Never put a service-account JSON/private key in the frontend.
- Product prices and stock used for order totals are re-read by Cloud Functions; client-submitted prices are ignored.
- Customers cannot write orders, rewards, vouchers, quiz answers/results or admin claims directly under Firestore rules.
- Historical order items store the product image URL at purchase time.

## Remaining production operations
Payment gateways are intentionally not represented as “paid” integrations: bKash/Nagad here are manual-payment collection fields. For automated payment confirmation, connect the official merchant gateway/webhook before treating an order as paid.
