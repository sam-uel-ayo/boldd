---
icon: money-bill-simple-wave
---

# Virtual Accounts (Dedicated NUBANs)

Provide dedicated bank account numbers to your customers. Deposits made into these accounts will automatically credit your main Boldd wallet, allowing you to build automated wallet systems.

### Allocation & Setup Flow

{% stepper %}
{% step %}
#### Query Banks

Check which banking partners are currently available for virtual account allocation. Get Available Banks
{% endstep %}

{% step %}
#### Setup Preferred Default

Configure which bank you prefer to route NUBAN generations through. Setup Preferred Bank
{% endstep %}

{% step %}
#### Generate Account

Allocate a unique dedicated NUBAN linked to the customer's profile reference. Generate Account
{% endstep %}
{% endstepper %}

### Available Endpoints

<table data-view="cards"><thead><tr><th>Endpoint</th><th data-type="content-ref"></th><th>Description</th><th data-hidden data-card-target data-type="content-ref">Link</th></tr></thead><tbody><tr><td><strong>Get Available Banks</strong></td><td><a href="get-available-banks.md">get-available-banks.md</a></td><td>Query supported partner banks for NUBAN generation.</td><td></td></tr><tr><td><strong>Setup Preferred Bank</strong></td><td><a href="setup-preferred-bank.md">setup-preferred-bank.md</a></td><td>Configure default banking routing choices for account generation.</td><td></td></tr><tr><td><strong>Generate Account</strong></td><td><a href="./#generate-account">#generate-account</a></td><td>Generate a dedicated NUBAN mapped to a customer's ID.</td><td></td></tr><tr><td><strong>Virtual Account List</strong></td><td><a href="virtual-account-list.md">virtual-account-list.md</a></td><td>Retrieve all virtual NUBAN profiles created under your account.</td><td></td></tr><tr><td><strong>Account Transactions</strong></td><td><a href="account-transactions.md">account-transactions.md</a></td><td>Audit real-time incoming transfer histories.</td><td></td></tr><tr><td><strong>Detach Account</strong></td><td><a href="detach-account.md">detach-account.md</a></td><td>Deactivate or remove virtual NUBAN routings from a customer.</td><td></td></tr><tr><td><strong>Virtual Account Webhook</strong></td><td><a href="virtual-account-webhook.md">virtual-account-webhook.md</a></td><td>Set up webhook endpoints to catch real-time deposit confirmations.</td><td></td></tr></tbody></table>
