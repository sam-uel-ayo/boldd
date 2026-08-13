---
icon: sliders
---

# Configuration

System configuration parameters, API environment URLs, security keys, rate limits, and webhook event specifications for the **Boldd Financial API Platform**.

***

## Environment Base URLs

Boldd provides dual environment access to ensure seamless testing prior to production launch:

```
# Staging / Sandbox Base URL
https://api.oneappgo.com/v1

# Production Base URL
https://api.oneappgo.com/v1
```

> [!NOTE]
> Environment selection is controlled by the secret key passed in the `Authorization` header. Sandbox secret keys (`sec_test_...`) route requests to sandbox ledgers, while live secret keys (`sec_live_...`) execute live banking operations.

***

## Secret Key Format & Management

| Key Type | Prefix | Recommended Usage |
| --- | --- | --- |
| **Sandbox Secret Key** | `sec_test_` | Integration testing, automated unit tests, staging environments. |
| **Live Secret Key** | `sec_live_` | Production server deployments, live billing, live card operations. |

```http
Authorization: Bearer sec_live_9a8b7c6d5e4f3a2b1c0d9e8f
```

***

## Webhook Event Specifications

Boldd sends real-time HTTP `POST` callbacks to your application backend whenever status updates occur (such as a successful card charge, virtual account deposit, or card refund).

### Top-Level Event Types (`event_type`)

| Event Type | Description |
| --- | --- |
| `TRANSACTIONS` | A payment was received via dedicated virtual account (NUBAN), payment link, or API checkout. |
| `REFUND` | A refund or reversal was processed for a payment or card transaction. |

### Channel Discriminators (`paid_through`)

Inspect the **`paid_through`** field in the `data` object to determine the transaction source:

| `paid_through` Value | Payment Channel Source |
| --- | --- |
| `dedicatedAccount` | Inbound bank transfer to a Virtual Account / Dedicated NUBAN. |
| `paylink` | Online checkout payment via `BolddCheckout()` modal or payment link. |
| `virtualcard` | Virtual card transaction or lifecycle operation. |

### Card Event Types (`type` / `normalized_type`)

For card transactions, inspect the `type` or `normalized_type` field in the webhook payload:

| Event Type | Description |
| --- | --- |
| `virtualcard_authorization` | Approved card purchase / POS spend. |
| `virtualcard_declined` | Declined card transaction attempt (e.g. insufficient card funds). |
| `virtualcard_refund` | Reversal or merchant refund back to card balance. |
| `virtualcard_topup` | Card funding load from operational wallet. |
| `virtualcard_withdrawal` | Card funds withdrawal back to operational wallet. |
| `virtualcard_termination` | Card termination and balance liquidation. |

### Sample Webhook Payload Format

```json
{
  "event_type": "transactions",
  "data": {
    "trans_status": "06",
    "message": "Successful",
    "transmode": "live",
    "feeby": "split",
    "reference": "1B6579758742351347",
    "paid_through": "dedicatedAccount",
    "TransDetails": {
      "transref": "1B6579758742351347",
      "clientref": "",
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

### Webhook Delivery & Retry Schedule
Your listener must respond with an HTTP `200 OK` within 5 seconds. If your server is unreachable or returns a non-200 status code:
* **Retry Schedule:** Retries automatically every **30 minutes for 48 hours**.
* **Notification History Log:** Outbound webhooks are logged in `transhook` and retrievable via `GET {{base_url}}/webhookevents.php` (or `POST {{base_url}}/webhookevents`).
* **Manual Repush:** Use `/business/repushnotification` to manually trigger a re-send.

***

## System Rate Limits & Quotas

To protect infrastructure stability, rate limits apply per merchant account:

| Rate Limit Level | Requests Per Second (RPS) | Burst Allowance |
| --- | --- | --- |
| **Sandbox / Staging** | 10 RPS | 20 Requests |
| **Production (Standard)** | 50 RPS | 100 Requests |
| **Production (Enterprise)** | Custom (up to 500 RPS) | Custom |

When limits are exceeded, the API responds with HTTP `429 Too Many Requests` containing the header `Retry-After: <seconds>`.

***

## Test Environment Mocking Data

When testing in the Sandbox environment using `sec_test_` keys:

* **Test BVN:** `22222222222` (Simulates valid Tier 1 KYC verification)
* **Test NIN:** `11111111111` (Simulates valid identity check)
* **Test Card Numbers:**
  * `4111 1111 1111 1111` (Visa - Always Succeeds)
  * `5100 0000 0000 0000` (Mastercard - Always Succeeds)
  * `5061 0000 0000 0000` (Verve - Always Succeeds)
  * `4000 0000 0000 0002` (Simulates Declined Transaction)
* **Test CVV:** Any 3 digits (`123`)
* **Test Expiry:** Any future date (`12/30`)
* **Test Virtual Account Inbound Credit:** Use the Sandbox test credit utility endpoint to simulate inbound bank transfers.
