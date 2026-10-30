# Bidora A–Z Marketplace

A Node.js marketplace starter with a broad A–Z department list, demo listings, account registration/login, seller listing uploads, live bidding with Socket.IO, and Razorpay order + signature verification.

## Requirements
- Node.js 20 or newer
- A Razorpay account for checkout (use TEST keys first)

## Run on Windows PowerShell
1. Extract this ZIP.
2. Open the extracted `Bidora-AZ-Marketplace` folder in VS Code.
3. Open Terminal → New Terminal.
4. Run:

```powershell
npm install
Copy-Item .env.example .env
```

5. Open `.env` and set a long random `JWT_SECRET`, plus your Razorpay **TEST** `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET`.
6. Start the server:

```powershell
npm start
```

7. Open http://localhost:8080

## Razorpay setup
- In the Razorpay Dashboard, switch to Test Mode and create API keys.
- Put the Key ID and Key Secret in `.env`.
- Restart the server after editing `.env`.
- The server creates an order and verifies the checkout signature before marking the order paid.
- Never put the Key Secret in frontend code, GitHub, or screenshots. Never use live keys until your merchant account is approved and your flow has been tested.

Without Razorpay keys, browsing, accounts, uploads and bidding work, but checkout returns a configuration message.

## Included features
- 20 seeded demo listings across departments
- Department filter and keyword search
- Buyer and seller registration
- Seller image upload (5 MB max)
- Live bid broadcasts to connected browsers
- Razorpay checkout order creation and server-side signature verification
- JSON file persistence in `data/bidora.json`

## Important limitations before production
This is a college-project starter, not a production commerce platform. Add robust database transactions, payment webhooks, inventory/auction closing jobs, email/SMS notifications, moderation, rate limiting, CSRF protections, image scanning/storage, privacy policy, refund/cancellation handling and security review before public commercial use. The starter stores JSON data locally; use a managed database and persistent object storage for deployment. Auction expiry is displayed but automatic winner settlement is not implemented.

## Buyer interest and public trust profile
- Every accepted bid is recorded as buyer interest against the seller's listing.
- Sellers can use the **Buyer interest** button to review bidders and the products they bid on.
- The public profile endpoint exposes only name, account type, completed purchase count and bid count. It does not expose email, password, phone number or other private account data.
- A bid is an expression of interest; it is not itself a completed purchase. Buyers use Buy Now / checkout for payment. Razorpay Test Mode credentials are required to test actual gateway checkout.

## Important payment notes
Set `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET` in `.env` using your own Razorpay TEST credentials. Never commit `.env` to GitHub. Use test credentials until your account and integration are ready for live payments. This demo is not a production marketplace; add order fulfilment, dispute handling, seller payout and stronger database/session controls before commercial use.

## Seller selection and buyer payment-request workflow

1. Register a buyer account and a separate seller account.
2. Sign in as the seller and publish an auction listing.
3. Sign in as the buyer in another browser/profile and place a bid.
4. Sign in as the seller and open **Buyer interest**. Review the buyer's public profile and choose **Select & request payment**.
5. The buyer opens **My orders** to see the payment request and chooses **Pay now**.
6. Configure Razorpay TEST credentials in `.env`; after checkout, the server verifies the Razorpay signature before marking the order paid.

The current application stores data in a local JSON file under `data/bidora.json` and uploads images under `uploads/`. These are suitable for a local demonstration but are not durable on many cloud hosts without persistent storage. Use HTTPS and a persistent database/storage service before production use. Public profiles expose only name, role, membership date, completed purchases and bid count.
