---
icon: book-open
---

# Reference

Welcome to the comprehensive technical reference for the **Boldd Financial API Platform**. This section provides complete specifications regarding API architecture, authentication protocols, global request/response headers, error codes, HTTP status mappings, security standards, and rate limiting policies.

***

## Platform Navigation

<table data-card-size="large" data-view="cards">
<thead>
<tr>
<th></th>
<th>Section</th>
<th>Description</th>
<th data-hidden data-card-target data-type="content-ref">Link</th>
</tr>
</thead>
<tbody>
<tr>
<td><h4>:sliders:</h4></td>
<td><strong>Configuration</strong></td>
<td>Environment URLs, HTTP headers, Webhook HMAC signatures, and rate limit tiers.</td>
<td><a href="configuration.md">Configuration</a></td>
</tr>
<tr>
<td><h4>:bookmark:</h4></td>
<td><strong>Glossary</strong></td>
<td>Exhaustive A–Z financial, compliance, card, and payment terminology definitions.</td>
<td><a href="glossary.md">Glossary</a></td>
</tr>
<tr>
<td><h4>:graduation-cap:</h4></td>
<td><strong>Integration Guides</strong></td>
<td>Detailed step-by-step walkthroughs for checkout, cards, virtual accounts, and KYC.</td>
<td><a href="guides.md">Guides</a></td>
</tr>
</tbody>
</table>

***

## API Architecture & Protocol

The Boldd API is designed as a RESTful web service communicating over encrypted HTTPS (TLS 1.2+ / TLS 1.3). All request payloads must be formatted as UTF-8 encoded JSON, and all responses are returned in JSON.

### Endpoint Structure
All API requests use the standardized host and version path prefix:
```
https://api.oneappgo.com/v1/business/{endpoint}
```

***

## Global Request Headers

Every HTTP request sent to the Boldd API requires the following headers:

| Header Name | Type | Required | Description / Example |
| --- | --- | --- | --- |
| `Authorization` | `string` | **Yes** | Secret key bearer token. Format: `Bearer sec_live_...` or `Bearer sec_test_...`. |
| `Content-Type` | `string` | **Yes** | Format of request payload. Must be `application/json`. |
| `Accept` | `string` | **Yes** | Expected response format. Set to `application/json`. |
| `X-Idempotency-Key` | `string` | **Optional** | Unique UUID v4 string to prevent duplicate processing of financial transactions. |

***

## Standard Response Structure

All API responses return a uniform JSON envelope containing a boolean `status`, a human-readable `msg`, and a payload `data` object or array.

### Successful Response Format (`200 OK`)
```json
{
  "status": true,
  "msg": "Transaction completed successfully",
  "data": {
    "reference": "REF_180507920200022257",
    "amount": 500000,
    "currency": "NGN",
    "status": "success",
    "created_at": "2026-08-13T16:50:00Z"
  }
}
```

### Error Response Format (`400` / `401` / `422` / `500`)
```json
{
  "status": false,
  "msg": "Insufficient funds in merchant operational wallet",
  "error_code": "INSUFFICIENT_FUNDS",
  "details": [
    {
      "field": "amount",
      "issue": "Requested transfer amount (500000) exceeds balance (120000)"
    }
  ]
}
```

***

## HTTP Status Codes

The API uses conventional HTTP status codes to indicate the outcome of an API request:

| Status Code | Meaning | Cause & Recommended Action |
| --- | --- | --- |
| `200 OK` | Success | Request succeeded. Refer to `data` for the payload. |
| `201 Created` | Created | Resource successfully created (e.g. customer, sub-account, card). |
| `400 Bad Request` | Client Error | Malformed JSON or missing required fields. Check parameter types. |
| `401 Unauthorized` | Auth Error | Missing, invalid, or expired Secret Key in `Authorization` header. |
| `403 Forbidden` | Access Denied | Key lacks permissions or IP address is not whitelisted. |
| `404 Not Found` | Not Found | Requested endpoint or resource ID does not exist. |
| `409 Conflict` | Duplicate | Transaction reference already exists (Idempotency conflict). |
| `422 Unprocessable Entity` | Validation Error | Payload is valid JSON but fails business rule validation (e.g. invalid BVN). |
| `429 Too Many Requests` | Rate Limited | Request threshold exceeded. Exponential backoff recommended. |
| `500 Internal Server Error` | Server Error | An error occurred on Boldd servers. Retry with backoff. |
| `502 / 503 Service Unavailable` | Provider Error | Upstream banking/card network temporarily unavailable. |

***

## Standardized Error Codes

When `status` is `false`, `error_code` provides a machine-readable string identifier:

| Error Code | Description |
| --- | --- |
| `INVALID_AUTHORIZATION` | Secret key is invalid, revoked, or formatted incorrectly. |
| `INSUFFICIENT_FUNDS` | Merchant or card account has insufficient funds to complete transaction. |
| `LIMIT_EXCEEDED` | Daily, monthly, or transaction limit exceeded for customer tier. |
| `CARD_BLOCKED` | Physical or virtual card is frozen, terminated, or restricted. |
| `KYC_REQUIRED` | Operation requires a higher KYC tier (e.g. Full KYC for Physical Cards). |
| `DUPLICATE_REFERENCE` | Provided `reference` or `trackingid` has already been processed. |
| `ACCOUNT_DISABLED` | Virtual account or sub-account has been detached or deactivated. |
| `PROVIDER_TIMEOUT` | Upstream partner bank or payment processor timed out. |
| `RESOURCE_NOT_FOUND` | Specified card, customer, or transaction ID does not exist. |
| `MAINTENANCE_MODE` | Endpoint is undergoing scheduled partner network maintenance. |

***

## Idempotency & Safety

For write operations that create charges, issue cards, or execute fund transfers, send a unique `X-Idempotency-Key` header (UUID v4) or unique transaction `reference`. If a network retry occurs with the same key within 24 hours, Boldd returns the original cached result without re-executing the financial transaction.

***

## Security & PCI Compliance

1. **Key Confidentiality:** Never expose secret keys (`sec_live_...`) in client-side code, frontend repositories, or mobile app binaries.
2. **PCI-DSS Tokenization:** Boldd handles card PCI compliance. Card primary account numbers (PANs) and CVVs are tokenized and accessible only via secure PCI-compliant views.
3. **Webhook Verification:** Verify all incoming webhooks using the HMAC SHA-256 signature generated with your webhook secret.
