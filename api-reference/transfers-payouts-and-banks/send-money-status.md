# Send Money Status

If a transfer was accepted but you didn't receive the final response (webhook missed, request timed out), use this to look up the real outcome — **don't blindly retry the transfer itself**.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/sendmoney-status`

**Request Headers**

<table><thead><tr><th width="155.66668701171875">Header</th><th width="108.33331298828125">Type</th><th width="107.3333740234375">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>Authorization</code></td><td><code>String</code></td><td>Yes</td><td>Bearer token authentication (e.g. <code>Bearer YOUR_SECRET_KEY</code>).</td></tr><tr><td><code>Content-Type</code></td><td><code>String</code></td><td>Yes</td><td>Request body format (e.g. <code>application/json</code>).</td></tr></tbody></table>

#### Request Body

| Field       | Type   | Required | Description                                   |
| ----------- | ------ | -------- | --------------------------------------------- |
| `reference` | string | Yes      | The reference sent with the original transfer |
| `txref`     | string | No       | Transaction reference, if available           |
| `provref`   | string | No       | Provider reference, if available              |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/sendmoney-status.php' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "reference": "API17828953589M105"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/sendmoney-status.php', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ reference: 'API17828953589M105' })
});
const data = await response.json();
```
{% endcode %}
{% endtab %}
{% endtabs %}

**Response fields:** `status`, `message`, `responsecode`, `reason_code`, `reason`, `responseStatus`, `deliveryStatus`, `reference`, `txref`, `retry_after_seconds`, `data.retryable`, `data.bank_name`, `data.bank_code`, `data.matched_reference`, `data.matched_timed`, `data.matched_amount`, `data.matched_accountno`

{% hint style="info" %}
`data.retryable` tells you whether it's safe to retry the transfer, or whether it already went through and retrying would create a duplicate payment.
{% endhint %}
