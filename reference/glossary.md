---
description: Comprehensive A-Z financial, compliance, card, and payment API term definitions.
icon: bookmark
---

# Glossary

Exhaustive, plain-language definitions of terms, parameters, status codes, and financial concepts used across the **Boldd API Platform** and Merchant Dashboard.

***

## A — C

<details>
<summary><strong>Account Number / Dedicated NUBAN</strong></summary>

A unique 10-digit bank account number generated dynamically or statically for a customer, sub-account, or wallet. Inbound transfers sent to a NUBAN are automatically credited to the merchant's ledger.
</details>

<details>
<summary><strong>Airtime Topup</strong></summary>

Mobile credit purchase for prepaid cellular networks (e.g. MTN, Airtel, Glo, 9mobile) executed via the Value-Added Services (VAS) endpoints.
</details>

<details>
<summary><strong>API Key / Secret Key</strong></summary>

A sensitive cryptographic token used to authenticate API requests. Passed in headers as `Authorization: Bearer sec_live_...` or `Authorization: Bearer sec_test_...`.
</details>

<details>
<summary><strong>Authorization Header</strong></summary>

The standard HTTP request header containing Bearer secret key credentials to authenticate API calls.
</details>

<details>
<summary><strong>Base URL</strong></summary>

The root path for all HTTP API requests. Standardized as `https://api.oneappgo.com/v1`.
</details>

<details>
<summary><strong>Bearer Token</strong></summary>

An HTTP authentication scheme where access is granted to whoever holds the token string in the header.
</details>

<details>
<summary><strong>Biometric Liveness Check</strong></summary>

A facial verification process that captures a short video or 3D facial scan to confirm that a live human is completing identity onboarding.
</details>

<details>
<summary><strong>BVN (Bank Verification Number)</strong></summary>

An 11-digit biometric identity number issued by the Central Bank of Nigeria used to verify customer identities during Tier 1 KYC checks.
</details>

<details>
<summary><strong>Cable TV Purchase (IUC / Smartcard)</strong></summary>

Subscription renewal for digital television providers (DSTV, GOTV, Startimes) using verified IUC or Smartcard numbers.
</details>

<details>
<summary><strong>Card Activation</strong></summary>

The API process (`card-activation`) that transforms a delivered physical debit card from an unactivated fulfillment state into an active, spendable card with an ATM PIN.
</details>

<details>
<summary><strong>Card Funding</strong></summary>

Transferring funds from a merchant operational balance directly into a specific virtual or physical card balance.
</details>

<details>
<summary><strong>Card Request Status</strong></summary>

The tracking state (`vcard-request-status`) of a physical card order during printing, batching, shipping, and courier delivery.
</details>

<details>
<summary><strong>Card Statement</strong></summary>

An itemized transaction ledger endpoint (`card-statement` / `card-statement.php`) returning card activity logs for virtual and physical cards, supporting date filtering up to 3 months (`from_date`, `to_date`, `months`, `duration_months`).
</details>

<details>
<summary><strong>Card Withdrawal</strong></summary>

Moving available funds out of a virtual or physical card back into the main merchant wallet (`vcard-withdraw`).
</details>

<details>
<summary><strong>Chargeback & Dispute</strong></summary>

A claim filed by a cardholder contesting a transaction. Managed via the Dispute Management endpoints (`fetch-disputes`, `accept-a-dispute`, `decline-a-dispute`).
</details>

<details>
<summary><strong>Customer Tier 1 vs Full KYC</strong></summary>

* **Tier 1:** Basic onboarding requiring valid name, phone number, and verified BVN or NIN.
* **Full KYC:** Advanced onboarding requiring proof of address, verified identity documents, and completed Liveness Check. Mandatory for Physical Card issuance.
</details>

***

## D — M

<details>
<summary><strong>Detach Account</strong></summary>

Deactivating or removing a virtual account number (`detach-virtualaccount` / `disable-accountno`) from an active customer profile.
</details>

<details>
<summary><strong>Electricity Biller (Meter Number Verification)</strong></summary>

Utility bill payment endpoint for purchasing prepaid electricity tokens or paying postpaid utility bills across discos.
</details>

<details>
<summary><strong>Inline / Popup Checkout (`BolddCheckout()`)</strong></summary>

A lightweight client-side JavaScript payment widget allowing merchants to collect card and bank transfer payments inside a modal popup.
</details>

<details>
<summary><strong>ISO 4217 Currency Codes</strong></summary>

Standardized 3-letter currency identifiers supported across balances and global accounts (e.g. `NGN`, `USD`, `EUR`, `MXN`).
</details>

<details>
<summary><strong>KYC (Know Your Customer)</strong></summary>

Mandatory regulatory identity verification procedures performed prior to enabling banking services or card issuance.
</details>

<details>
<summary><strong>Multi-Tenancy & Sub-Accounts</strong></summary>

An architectural framework allowing platform merchants to create sub-accounts, attach custom payout accounts, and manage split settlements.
</details>

***

## N — Z

<details>
<summary><strong>NIN (National Identification Number)</strong></summary>

An 11-digit national identity number issued by NIMC used for identity verification checks in Nigeria.
</details>

<details>
<summary><strong>Operational Wallet / Balance</strong></summary>

The central pool of funds held in a merchant's account used to issue cards, fund accounts, execute payouts, and settle transactions.
</details>

<details>
<summary><strong>Physical Card</strong></summary>

A plastic or metal debit card linked to a customer ledger, enabled for physical Point-Of-Sale (POS) purchases and ATM cash withdrawals.
</details>

<details>
<summary><strong>PIN (Personal Identification Number)</strong></summary>

A 4-digit secret passcode used by cardholders to authorize physical card POS/ATM transactions or virtual card security operations (`update-card-pin`).
</details>

<details>
<summary><strong>Repush Notification</strong></summary>

An API operation (`/business/repushnotification`) that manually triggers a re-send of a missing or failed webhook event notification.
</details>

<details>
<summary><strong>Sandbox Environment</strong></summary>

A isolated test environment using `sec_test_` keys, test bank accounts, and mock card numbers to safely test API integrations.
</details>

<details>
<summary><strong>Settlement & Payout</strong></summary>

The transfer of collected payment funds from Boldd merchant ledgers to a registered commercial bank account.
</details>

<details>
<summary><strong>Universal Blacklist</strong></summary>

A centralized security registry used to flag and block fraudulent BVNs, accounts, cards, or IP addresses from interacting with the platform.
</details>

<details>
<summary><strong>Virtual Card</strong></summary>

A digital payment card (Visa/Mastercard/Verve) generated instantly via API for online shopping, cloud subscriptions, and global digital payments.
</details>

<details>
<summary><strong>Webhook</strong></summary>

An automated HTTP `POST` notification sent by Boldd servers to a merchant's backend server whenever a transaction, deposit, or card event occurs.
</details>
