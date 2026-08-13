---
icon: sliders
---

# Configuration

System parameters, environment settings, service grants, quotas, pricing overrides, and webhook event specifications for the **Boldd API Platform**.

***

## Base URL

Prefix every endpoint in the reference with:
```
{{base_url}} = https://api.oneappgo.com/v1
```

***

## Authentication & Key Types

Boldd authenticates requests via the `Authorization` header:

```http
Authorization: Bearer YOUR_SECRET_KEY
```
or
```http
Authorization: Bearer YOUR_PUBLIC_KEY
```

* **Secret Key:** Authorized to execute state-changing actions (initializing transactions, sending money, issuing cards). Keep strictly confidential on your backend.
* **Public Key:** Used for read-only scenarios (e.g. fetching bank lists, data plans, electricity billers).
* **Test vs. Live Mode:** Determined by the key used (`1applive_sk_...` vs test keys). Data between test and live mode is fully isolated.

***

## Service Grants

Certain endpoints check for an explicit grant on your account in addition to key validation:

| Grant Name | Feature / Endpoint Coverage |
| --- | --- |
| `virtualcard` | Virtual card creation and management |
| `sendmoney` | Bank transfer payouts |
| `globalaccount` | Global FX account creation |
| `virtualaccount` | Dedicated NUBAN virtual account generation |
| `usdaccount` | USD account issuance |
| `ngnusd` | NGN to USD conversion |
| `bvn_kyc` | BVN identity verification checks |
| `nin_kyc` | NIN identity verification checks |
| `liveness` | Biometric liveness check sessions |

To request access to any of these service grants, email **hi@useboldd.com**. If a grant is missing, the API returns a safe failure payload with `"status": false`.

***

## Usage Quotas & Metered Endpoints

The following endpoints are covered by quota policies and may return advisory usage fields in `data`:

* **Metered Products:** `sendmoney`, `sendmoney-status`, `virtualcard`, `globalaccount`, `bvn_kyc`, `nin_kyc`, `verifybankacct`, `verifyelect`, `liveness`, `verifytrans`, `cardrequest-status`.

| Advisory Field | Description |
| --- | --- |
| `free_limit` | Free usage allowance for the current window. |
| `current_count` | Usage count so far in the current window. |
| `overage_fee` | Fee charged once `free_limit` is exceeded. |

***

## Pricing Overrides Configuration Fields

Configurable account pricing fields (`api_service_pricing`):
* `platform_fee`, `platform_fee_value`, `platform_fee_mode`
* `card_creation_fee`, `card_funding_fee_percent`, `card_funding_fee_cap`, `card_termination_fee_percent`, `card_termination_fee_cap`
* `monthly_fee_per_card_after_limit`, `monthly_fee_free_limit`
* `chargeback_fee`, `decline_fee`, `free_limit`, `overage_fee`, `cap`

***

## Status & Retry Lookup Endpoints

Rather than blindly retrying a failed transfer or card request, use the matching status/retry endpoint:

| Action | Status Lookup Endpoint |
| --- | --- |
| **Send Money Status** | `POST {{base_url}}/business/sendmoney-status.php` |
| **Payment Status** | `POST {{base_url}}/checktrans-status` |
| **Physical Card Request Status** | `POST {{base_url}}/business/cardrequest-status` |
| **Virtual Card Request Status** | `POST {{base_url}}/business/vcard-request-status` |

***

## Webhook Event Specifications

Boldd sends real-time HTTP `POST` callbacks to your registered URL when status updates occur.

### Event Types (`event_type`)

| Event Type | Description |
| --- | --- |
| `TRANSACTIONS` | Payment received via virtual account, payment link, or checkout. |
| `REFUND` | Refund or reversal processed for a payment or card transaction. |

### Channel Discriminators (`paid_through`)

| `paid_through` Value | Channel Source |
| --- | --- |
| `dedicatedAccount` | Inbound bank transfer to a Virtual Account / Dedicated NUBAN. |
| `paylink` | Online payment via checkout payment link or modal. |
| `virtualcard` | Virtual card transaction or issuance event. |

### Card Event Types (`type` / `normalized_type`)

* `virtualcard_authorization` (Approved card spend)
* `virtualcard_declined` (Declined card spend attempt)
* `virtualcard_refund` (Card refund / reversal)
* `virtualcard_topup` (Card funding load)
* `virtualcard_withdrawal` (Card funds withdrawal to wallet)
* `virtualcard_termination` (Card termination)

### Sample Webhook Payload
```json
{
  "event_type": "transactions",
  "data": {
    "trans_status": "06",
    "message": "Successful",
    "transmode": "live",
    "feeby": "split",
    "reference": "1B6579758742351347",
    "paid_through": "paylink",
    "TransDetails": {
      "transref": "1B6579758742351347",
      "amountpaid": "10000.00",
      "amount_settled": "9950.00",
      "fee": "50.00",
      "currency": "NGN",
      "previous_bal": "100000.00",
      "new_bal": "19950.00",
      "payment_time": "Sat, 16 Jul 2026"
    },
    "CustomerDetails": {
      "customer_name": "John Doe",
      "customer_email": "johndoe@example.com",
      "customer_phone": "0701234567"
    }
  }
}
```

### Delivery & Retry Policy
* Endpoint must acknowledge with an HTTP `200 OK` within 5 seconds.
* If delivery fails, Boldd retries for **48 hours at 30-minute intervals**.
* Outbound webhooks are logged in `transhook` and retrievable via `GET {{base_url}}/webhookevents.php` (or `POST {{base_url}}/webhookevents`).
* Manual repush can be triggered via `POST {{base_url}}/business/repushnotification`.
