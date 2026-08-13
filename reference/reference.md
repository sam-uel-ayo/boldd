---
icon: book-open
---

# Reference

Technical reference and core specifications for the **Boldd API Platform**.

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
<td>Base URL, authentication headers, service grants, quotas, pricing fields, and webhook specs.</td>
<td><a href="configuration.md">Configuration</a></td>
</tr>
<tr>
<td><h4>:bookmark:</h4></td>
<td><strong>Glossary</strong></td>
<td>Definitions of terms, KYC tiers, response codes, and endpoints used across the docs.</td>
<td><a href="glossary.md">Glossary</a></td>
</tr>
<tr>
<td><h4>:graduation-cap:</h4></td>
<td><strong>Integration Guides</strong></td>
<td>Walkthroughs for payments, virtual accounts, cards, identity verification, and webhooks.</td>
<td><a href="guides.md">Guides</a></td>
</tr>
</tbody>
</table>

***

## Base URL & Endpoint Structure

All API requests must use the base URL:
```
{{base_url}} = https://api.oneappgo.com/v1
```

***

## HTTP Request Headers

| Header Name | Type | Required | Description |
| --- | --- | --- | --- |
| `Authorization` | `string` | **Yes** | Bearer secret or public key token (`Bearer YOUR_SECRET_KEY` or `Bearer YOUR_PUBLIC_KEY`). |
| `Content-Type` | `string` | **Yes** | Payload format. Must be `application/json`. |

***

## Response Envelope & Validation Handling

Every Boldd API response returns a consistent JSON envelope:

```json
{
  "status": false,
  "message": "No card selected!",
  "responsecode": "00",
  "missing_fields": ["cardid"],
  "received_fields": ["updatetype"],
  "data": []
}
```

| Field | Type | Description |
| --- | --- | --- |
| `status` | `boolean` | `true` for clean success, `false` for failure or blocked operation. |
| `message` | `string` | Human-readable explanation of the result. |
| `responsecode` | `string` | Machine-readable outcome code. |
| `data` | `array` / `object` | Result payload. Check `status` first (an empty array `[]` does not automatically mean an error). |
| `missing_fields` | `array` | Returned on validation failures — lists required fields you omitted. |
| `received_fields` | `array` | Returned on validation failures — lists the fields sent to the server. |

***

## Transaction Response Codes (`responsecode`)

| Code | Meaning | Description |
| --- | --- | --- |
| `00` | Unconfirmed / Failed | General failure, unconfirmed state, or unauthorized access. |
| `01` | Successful | Payment or action authorized and completed. |
| `02` | Underpaid | Payment received but amount paid was less than expected (reconciliation required). |
| `03` | Overpaid | Payment received but amount paid exceeded expected (reconciliation required). |
| `04` | Refunded | Payment was successfully refunded. |
| `05` | Cancelled | Payment was cancelled by user or system before completion. |
| `06` | Failed / Not Found | Payment failed or requested resource (e.g. Virtual Account) was not found. |

***

## HTTP Status Codes

| Status Code | Description |
| --- | --- |
| `200 OK` | Request processed. Note: Most Boldd API responses (even application errors) return `200 OK` with a `"status": false` payload. |
| `400 Bad Request` | Request unacceptable due to missing parameters or invalid formatting. |
| `401 Unauthorized` | Missing or invalid API key, or using a Test Key on a Live-only endpoint. |
| `403 Forbidden` | API key lacks permission or missing required Service Grant. |
| `404 Not Found` | Requested resource or endpoint does not exist. |
| `500 Server Error` | Unexpected internal server error. |

***

## Common Error Messages

* `"Invalid Authorization Key"` — Missing, malformed, or wrong key environment.
* `"Duplicate transaction reference"` — The transaction `reference` has already been used.
* `"Insufficient balance on merchant account"` — Wallet balance is too low for the request.
* `"You are currently not eligible to access this resources"` — Account requires a Service Grant or higher KYC tier.
