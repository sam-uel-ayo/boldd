---
icon: message-code
---

# Response Code & Errors

Every Boldd API response follows a consistent envelope, whether the request succeeds or fails.

### Response Envelope

<table><thead><tr><th width="160.66668701171875">Field</th><th>Description</th></tr></thead><tbody><tr><td><code>status</code></td><td><code>true</code> for success, <code>false</code> for failure</td></tr><tr><td><code>message</code></td><td>Human-readable description of the result</td></tr><tr><td><code>responsecode</code></td><td>Machine-readable outcome code (see table below)</td></tr><tr><td><code>data</code></td><td>The response payload. An empty array <code>[]</code> does not mean an error — always check <code>status</code> first</td></tr><tr><td><code>missing_fields</code></td><td>Present on validation failures — lists required fields you didn't send</td></tr><tr><td><code>received_fields</code></td><td>Present on validation failures — lists the fields you actually sent, useful for debugging payload mismatches</td></tr></tbody></table>

**Example - validation failure:**

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

**Example - success:**

```json
{
  "status": true,
  "message": "Successful",
  "responsecode": "01",
  "data": []
}
```

#### Response Codes

<table><thead><tr><th width="159.3333740234375">Code</th><th>Meaning</th></tr></thead><tbody><tr><td><code>00</code></td><td>Unconfirmed / pending</td></tr><tr><td><code>01</code></td><td>Successful</td></tr><tr><td><code>02</code></td><td>Successful but underpaid (reconciliation required)</td></tr><tr><td><code>03</code></td><td>Successful but overpaid (reconciliation required)</td></tr><tr><td><code>04</code></td><td>Refunded</td></tr><tr><td><code>05</code></td><td>Cancelled</td></tr><tr><td><code>06</code></td><td>Failed</td></tr></tbody></table>

#### How to Handle Responses

1. **Check `status` first** — `status: true` indicates a clean success with no reconciliation issue.
2. **Inspect `payment_status` for dynamic transfers** — `status: false` does not always mean no money was received. For dynamic transfer confirmations:
   * If `payment_status: true` and `responsecode` is `02` (underpaid) or `03` (overpaid), the payment was received but the amount paid did not match the expected amount. Inspect `amount_difference` and `reconciliation_required`.
3. **Use `responsecode`** to branch on the specific transaction outcome (pending vs. successful vs. underpaid/overpaid vs. failed vs. refunded).
4. **Display `message`** to your user or your logs.
5. **Use `missing_fields`** to drive form validation prompts in your own UI.
6. **Use `received_fields`** when debugging — it shows exactly what reached the server, which catches typos in field names on your end.

### Standard HTTP Status Codes

<table data-header-hidden><thead><tr><th width="103.6666259765625"></th><th width="163.333251953125"></th><th></th></tr></thead><tbody><tr><td><strong>Code</strong></td><td><strong>Status</strong></td><td><strong>Description</strong></td></tr><tr><td><strong>200</strong></td><td><code>OK</code></td><td>Everything worked as expected. Most Boldd API responses (even application-level errors) return a <code>200 OK</code> with a <code>status: false</code> payload.</td></tr><tr><td><strong>400</strong></td><td><code>Bad Request</code></td><td>The request was unacceptable, often due to missing a required parameter or invalid formatting.</td></tr><tr><td><strong>401</strong></td><td><code>Unauthorized</code></td><td>No valid API key provided, or you are using a Test Key for a Live-only endpoint.</td></tr><tr><td><strong>403</strong></td><td><code>Forbidden</code></td><td>The API key doesn't have permissions to perform the request.</td></tr><tr><td><strong>404</strong></td><td><code>Not Found</code></td><td>The requested resource doesn't exist.</td></tr><tr><td><strong>500</strong></td><td><code>Server Error</code></td><td>Something went wrong on our end.</td></tr></tbody></table>

### API Status Flag (`status`)

All JSON responses from the Boldd API contain a boolean `status` field. You should check this flag first before processing the rest of the payload.

* `"status": true`: The operation was successful.
* `"status": false`: The operation failed or was blocked (e.g., insufficient balance, duplicate reference, invalid key). Always check the accompanying `"message"` field for details.

### Transaction Response Codes (`responsecode`)

When initializing, verifying, or fetching the status of a payment, transfer, or virtual card transaction, look for the `"responsecode"` field in the `data` object to determine the exact state of the transaction.

<table data-header-hidden><thead><tr><th width="164.6666259765625"></th><th></th></tr></thead><tbody><tr><td><strong>Response Code</strong></td><td><strong>Description</strong></td></tr><tr><td><code>00</code></td><td><strong>Failed / Unconfirmed:</strong> Indicates a general failure, an unconfirmed status, or unauthorized access (e.g., "Invalid Authorization Key").</td></tr><tr><td><code>01</code></td><td><strong>Successful:</strong> Payment Authorized and Successful. Value has been delivered.</td></tr><tr><td><code>04</code></td><td><strong>Refunded:</strong> The payment was successfully refunded to the customer.</td></tr><tr><td><code>05</code></td><td><strong>Cancelled:</strong> The payment was cancelled by the user or the system before completion.</td></tr><tr><td><code>06</code></td><td><strong>Failed / Not Found:</strong> The payment failed or the requested resource (e.g., Virtual Account) could not be found.</td></tr></tbody></table>

### Common Error Messages

Below are common error messages you might encounter in the `"message"` field when `"status": false`:

* `"Invalid Authorization Key"` - Your Bearer token is missing, malformed, or incorrect for the requested environment.
* `"Duplicate transaction reference"` - You are trying to process a transaction with a `reference` that has already been used.
* `"Insufficient balance on merchant account"` - Your wallet balance is too low to cover the requested transfer or VAS purchase.
* `"You are currently not eligible to access this resources"` - Your account requires further compliance approval (e.g., Full KYC) before using premium features like Virtual Accounts or USD Global Accounts.

