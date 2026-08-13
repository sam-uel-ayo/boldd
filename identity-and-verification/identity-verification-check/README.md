---
icon: id-card
---

# Identity Verification Check

Confirm user identities and meet KYC regulatory compliance requirements using Boldd's verification APIs. We offer two main verification methods to programmatically confirm user details against national identity registries in Nigeria:

### Available Services

{% stepper %}
{% step %}
#### BVN Verification (Bank Verification Number)

Retrieve and verify customer bank registry records, including names, dates of birth, phone numbers, and profile photos. BVN Verification Guide
{% endstep %}

{% step %}
#### NIN Verification (National Identification Number)

Verify a customer's identity details directly against the National Identity Management Commission (NIMC) database. NIN Verification Guide
{% endstep %}
{% endstepper %}

### Verification Modes

Both checks are available in two operational modes depending on the depth of information required:

* **Basic Mode:** Performs a quick check confirming registry presence and returning basic profile details (e.g. name, phone number).
* **Premium Mode:** Retrieves the full registry record, including the registered address, date of birth, and profile image (base64 encoded photo).

{% hint style="info" %}
Identity verification checks require the appropriate service grant on your API key (`bvn_kyc` or `nin_kyc` checks). Check out the Service Access & Limits page for activation steps.
{% endhint %}
