---
icon: credit-card-blank
---

# Payments (Collections)

## Payments (Collections)

Boldd Collections APIs enable you to accept payments from customers globally. We support multiple payment channels, including local cards, bank transfers, USSD, and mobile money.

#### Payment Integration Flow

{% stepper %}
{% step %}
#### Initialize Transaction

Submit the customer details, amount, and reference to generate a checkout session. Initialize Payment
{% endstep %}

{% step %}
#### Present Checkout

Display the payment modal inline in your app or redirect the user to Boldd's checkout page. Inline/Popup Checkout
{% endstep %}

{% step %}
#### Verify Payment

Verify the settlement status on your server using webhook events or our query endpoints. Verify Payment
{% endstep %}
{% endstepper %}

#### Available Endpoints

<table data-view="cards"><thead><tr><th>Endpoint</th><th>Description</th><th data-hidden data-card-target data-type="content-ref">Link</th></tr></thead><tbody><tr><td><strong>Initialize Payment</strong></td><td>Prepare a payment request and obtain checkout redirect credentials.</td><td></td></tr><tr><td><strong>Inline/Popup Checkout</strong></td><td>Embed the visual overlay checkout gateway directly into your front-end.</td><td></td></tr><tr><td><strong>Verify Payment</strong></td><td>Query the definitive state of a transaction to deliver services.</td><td></td></tr><tr><td><strong>Payment List</strong></td><td>Search and audit historical collections logged under your account.</td><td></td></tr><tr><td><strong>Payment Details</strong></td><td>Fetch complete database records for a single payment.</td><td></td></tr><tr><td><strong>Payment Status</strong></td><td>Quickly query state indicators for a pending transaction.</td><td></td></tr></tbody></table>
