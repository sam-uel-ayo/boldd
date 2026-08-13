---
icon: gauge-simple-max
---

# Service Access & Limits

## Service Access & Limits

Some Boldd features require more than a valid API key — they also require a **service grant** on your business account, and some are subject to usage quotas.

#### Service Grants

Certain endpoints check for an explicit grant on your account in addition to key type. Current grantable services include:

* `virtualcard`
* `sendmoney`
* `globalaccount`
* `virtualaccount`
* `usdaccount`
* `ngnusd`&#x20;
* `bvn_kyc`
* `nin_kyc`
* `liveness`

To request access to any of these, email [**hi@useboldd.com**](mailto:hi@useboldd.com) with the service name(s) you need.

{% hint style="info" %}
If your business doesn't have a required service grant, the API returns a safe, normalized failure response rather than a blank or malformed payload — check `status` and `message` to see if a missing grant is the cause.
{% endhint %}

#### Usage Quotas & Overage Billing

Some products include a free usage window. Once you exceed it, the API either bills an overage fee automatically or returns a normalized rate-limit error, depending on the endpoint and your account's configured access model.

Products currently covered by quota policy:

`sendmoney` · `sendmoney-status` · `virtualcard` · `globalaccount` · `bvn_kyc` · `nin_kyc` · `verifybankacct` · `verifyelect` · `liveness` · `verifytrans` · `cardrequest-status`

**Advisory fields** you may see in `data` on metered endpoints:

| Field           | Description                                      |
| --------------- | ------------------------------------------------ |
| `free_limit`    | Your free usage allowance for the current window |
| `current_count` | Your usage so far in the current window          |
| `overage_fee`   | The fee charged once you exceed `free_limit`     |

#### Business Pricing Overrides

The API supports business-specific pricing overrides (`api_service_pricing`) with safe fallbacks to global defaults (`API_USAGE_POLICIES` and `API_SERVICE_PRICING_DEFAULTS`).

Configurable pricing fields for accounts include:

* `platform_fee`, `platform_fee_value`, `platform_fee_mode`
* `card_creation_fee`, `card_funding_fee_percent`, `card_funding_fee_cap`, `card_termination_fee_percent`, `card_termination_fee_cap`
* `monthly_fee_per_card_after_limit`, `monthly_fee_free_limit`
* `chargeback_fee`, `decline_fee`, `free_limit`, `overage_fee`, `cap`

#### Practical Rules for Consumers

* **Don't blindly retry a failed transfer or card request.** Call the matching status endpoint instead (**Send Money Status**, **Payment Status**, **Card Request Status**) to check what actually happened before resending.
* **If you get `status: false` with a rate-limit message**, stop retrying until your quota window resets or you upgrade access.
* Status/retry endpoints return a safe, normalized payload even when nothing is found, so you can distinguish "not found," "still processing," and a genuine transport failure.

**Status/retry endpoints:**

* `POST {{base_url}}/business/sendmoney-status.php` — send money status & retry lookup
* `POST {{base_url}}/checktrans-status` — payment status
* `POST {{base_url}}/business/cardrequest-status` — physical card request status
* `POST {{base_url}}/business/vcard-request-status` — virtual card request status
