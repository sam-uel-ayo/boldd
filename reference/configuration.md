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

## Webhook Architecture & Signature Verification

Boldd sends real-time HTTP `POST` notifications for transaction updates, card events, and account credits.

### Webhook Event Envelope Payload
```json
{
  "event": "vaccount.credited",
  "event_id": "evt_9876543210",
  "created_at": "2026-08-13T16:50:00Z",
  "data": {
    "account_number": "9912345678",
    "bank_name": "Wema Bank",
    "amount": "25000.00",
    "currency": "NGN",
    "session_id": "000013240813165000001",
    "payer_name": "CHIDI OKONKWO",
    "payer_account": "0123456789",
    "reference": "REF_TRANSFER_9912"
  }
}
```

### Supported Webhook Events

| Event Name | Trigger Condition |
| --- | --- |
| `payment.successful` | Inline or popup checkout payment completed and verified. |
| `payment.failed` | Payment attempt failed or declined by issuing bank. |
| `vaccount.credited` | Inbound bank transfer credited to a dedicated NUBAN virtual account. |
| `card.issued` | Virtual or physical card order successfully issued. |
| `card.debited` | Debit transaction executed on a card. |
| `card.credited` | Refund or funding transaction applied to a card. |
| `card.frozen` | Card status toggled to frozen. |
| `dispute.created` | Customer dispute or chargeback logged against a transaction. |
| `kyc.verified` | Customer Liveness Check or Full KYC verification completed. |

### HMAC SHA-256 Signature Verification
To verify that webhooks originate from Boldd and have not been tampered with, calculate the HMAC SHA-256 signature using your Webhook Secret Key and compare it with the `X-Boldd-Signature` header.

#### Node.js Verification Example
```javascript
const crypto = require('crypto');

function verifyWebhookSignature(rawBody, signatureHeader, secretKey) {
  const hash = crypto
    .createHmac('sha256', secretKey)
    .update(rawBody)
    .digest('hex');
  return hash === signatureHeader;
}
```

#### Python Verification Example
```python
import hmac
import hashlib

def verify_webhook_signature(raw_body_bytes, signature_header, secret_key):
    expected_hash = hmac.new(
        secret_key.encode('utf-8'),
        raw_body_bytes,
        hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(expected_hash, signature_header)
```

### Webhook Retry & Delivery Policy
If your endpoint fails to return an HTTP `200 OK` status (e.g. timeout, 5xx server error), Boldd retries delivery according to the following schedule:
* **Retry 1:** 5 minutes after initial attempt
* **Retry 2:** 15 minutes after initial attempt
* **Retry 3:** 1 hour after initial attempt
* **Retry 4:** 6 hours after initial attempt
* **Retry 5:** 24 hours after initial attempt

Manual webhook retries can be requested at any time using the [Repush Notification](../getting-started/webhooks-and-notifications/repush-notification.md) endpoint (`/business/repushnotification`).

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
