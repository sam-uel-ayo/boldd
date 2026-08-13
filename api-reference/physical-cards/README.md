---
icon: credit-card-front
---

# Physical Cards

Issue physical debit cards to your customers, track delivery statuses, and activate cards once they are in the customer's hands.

### Fulfillment Flow

{% stepper %}
{% step %}
#### Create Card

Submit a physical debit card request for a Full KYC customer. Create Card Guide
{% endstep %}

{% step %}
#### Card Request Status

Track delivery and printing status. Card Request Status Guide
{% endstep %}

{% step %}
#### Card Activation

Activate the card upon delivery. Card Activation Guide
{% endstep %}
{% endstepper %}

### Available Endpoints

<table data-view="cards"><thead><tr><th>Endpoint</th><th data-type="content-ref"></th><th>Description</th><th data-hidden data-card-target data-type="content-ref">Link</th></tr></thead><tbody><tr><td><strong>Create Card</strong></td><td><a href="create-card.md">create-card.md</a></td><td>Submit orders for physical cards for a Full KYC customer profile.</td><td></td></tr><tr><td><strong>Card Request Status</strong></td><td><a href="card-request-status.md">card-request-status.md</a></td><td>Track the shipping and delivery state of a physical card order.</td><td></td></tr><tr><td><strong>Card Activation</strong></td><td><a href="card-activation.md">card-activation.md</a></td><td>Activate physical cards to enable ATM and POS transactions.</td><td></td></tr><tr><td><strong>Cards Details</strong></td><td><a href="cards-details.md">cards-details.md</a></td><td>Fetch physical card metadata and ledger limits.</td><td></td></tr><tr><td><strong>Freeze and Unfreeze Card</strong></td><td><a href="freeze-and-unfreeze-card.md">freeze-and-unfreeze-card.md</a></td><td>Temporarily toggle card block status.</td><td></td></tr><tr><td><strong>Card Statement</strong></td><td><a href="../virtual-cards/card-statement.md">card-statement.md</a></td><td>Retrieve transaction statements for both virtual and physical cards (up to 3 months).</td><td></td></tr></tbody></table>

### Card Operations (Ongoing Lifecycle)

Manage active physical cards using the operational endpoints:

* **Cards Details:** Get full card metadata.
* **Freeze and Unfreeze Card:** Temporarily toggle card block status.
* **Card Statement:** Retrieve statements for auditing.
* **Update Card PIN:** Securely change card ATM PIN.
