---
icon: graduation-cap
---

# Guides

Comprehensive, self-contained integration guides for building production financial products on the **Boldd API Platform**.

***

## 1. Card Operations & Issuance Lifecycle

Implement end-to-end virtual and physical debit card issuance, funding, transactions, and statements.

* **[Virtual Card Account Creation](../api-reference/virtual-cards/create-card-account.md):** Set up dedicated virtual card accounts for end-users.
* **[Virtual Card Issuance](../api-reference/virtual-cards/cards-issuance.md):** Issue instant digital debit cards (Visa/Mastercard/Verve) for online e-commerce transactions.
* **[Card Funding](../api-reference/virtual-cards/card-funding.md):** Instantly fund card accounts from the merchant operational wallet.
* **[Card Withdrawal](../api-reference/virtual-cards/withdraw-card-funds.md):** Withdraw unused card funds back into operational balances.
* **[Physical Card Fulfillment & Shipping](../api-reference/physical-cards/README.md):** Request physical cards for Full KYC customers, track shipping printing statuses (`card-request-status`), and execute final delivery activation (`card-activation`).
* **[Card Statements](../api-reference/virtual-cards/card-statement.md):** Retrieve itemized transaction logs for both Virtual and Physical Cards with date range filters (`from_date`, `to_date`, `months` up to 3 months).

***

## 2. Virtual Accounts & Inbound Bank Collections

Generate dedicated virtual bank account numbers (NUBANs) for automated bank transfer collections.

* **[Get Available Partner Banks](../api-reference/virtual-accounts-dedicated-nubans/get-available-banks.md):** Query available settlement partner banks (e.g. Wema Bank, Providus, Sterling).
* **[Generate Virtual Account](../api-reference/virtual-accounts-dedicated-nubans/generate-account.md):** Dynamically generate static or dynamic NUBAN accounts assigned to specific customers.
* **[Account Transactions Audit](../api-reference/virtual-accounts-dedicated-nubans/account-transactions.md):** Audit incoming bank transfer ledger entries.
* **[Detach Virtual Account](../api-reference/virtual-accounts-dedicated-nubans/detach-account.md):** Safely deactivate or detach virtual accounts (`detach-virtualaccount`).

***

## 3. Payments & Inline Checkout

Integrate web payment checkout flows for credit/debit cards, bank transfers, and wallets.

* **[Initialize Payment Session](../api-reference/payments-collections/initialize-payment.md):** Generate checkout transaction tokens and payment links.
* **[Inline Popup Checkout Integration](../api-reference/payments-collections/inline-popup-checkout.md):** Embed the seamless `BolddCheckout()` JavaScript popup directly into your web app.
* **[Verify Payment Status](../api-reference/payments-collections/verify-payment.md):** Execute server-to-server verification for initialized payments.

***

## 4. Customer Onboarding & KYC Compliance

Verify identity and maintain regulatory compliance across onboarding tiers.

* **[Create Tier 1 Customer](../identity-and-verification/customers/create-customer-tier-1.md):** Perform lightweight onboarding using BVN/NIN verification.
* **[Full KYC Customer Upgrade](../identity-and-verification/customers/create-customer-full-kyc.md):** Upgrade customer profiles with full documentation to unlock physical card issuance and higher transaction limits.
* **[Liveness Check Verification](../identity-and-verification/liveness-check/create-liveness-session.md):** Initiate biometric liveness check sessions and handle callback notifications.

***

## 5. Transfers, Payouts & Settlements

Execute outbound transfers and manage merchant payouts.

* **[Bank List Query](../api-reference/transfers-payouts-and-banks/bank-list.md):** Fetch valid destination banks and bank routing codes.
* **[Account Name Lookup](../api-reference/transfers-payouts-and-banks/validate-account-name.md):** Perform real-time name verification on destination account numbers before sending funds.
* **[Send Money (Payout)](../api-reference/transfers-payouts-and-banks/send-money.md):** Execute automated bank transfer payouts.
* **[Payout Status Verification](../api-reference/transfers-payouts-and-banks/send-money-status.md):** Check real-time transfer settlement status (`sendmoney-status`).

***

## 6. Value-Added Services (VAS) & Utilities

Sell airtime, data bundles, and utility bill payments.

* **[Airtime & Data Topup](../api-reference/bills-payment-vas/data-plans.md):** Fetch data plans and execute instant mobile top-ups.
* **[Electricity Bills](../api-reference/bills-payment-vas/verify-meter-number.md):** Verify meter numbers and purchase electricity tokens.
* **[Cable TV Subscriptions](../api-reference/bills-payment-vas/verify-iuc.md):** Verify smartcard/IUC numbers and renew DSTV, GOTV, or Startimes packages.

***

## 7. Sub-Accounts & Multi-Tenant Platform Settlement

Manage multi-tenant platforms, sub-merchants, and fee splitting.

* **[Create Sub-Account](../api-reference/sub-accounts-and-multi-tenancy/create-a-sub-account.md):** Provision isolated merchant sub-accounts.
* **[Attach Bank & Payout Accounts](../api-reference/sub-accounts-and-multi-tenancy/attach-payout-account.md):** Configure automated settlement accounts for sub-merchants.
* **[Sub-Account Wallets & History](../api-reference/sub-accounts-and-multi-tenancy/sub-accounts-wallet.md):** Monitor sub-merchant balances and transaction ledgers.

***

## 8. Webhooks & Event-Driven Architecture

* **[Webhook Notifications](../getting-started/webhooks-and-notifications/webhook-notifications.md):** Configure secure webhook endpoints and process automated payload notifications.
* **[Repush Notification](../getting-started/webhooks-and-notifications/repush-notification.md):** Request manual webhook re-delivery for missing notifications (`/business/repushnotification`).
