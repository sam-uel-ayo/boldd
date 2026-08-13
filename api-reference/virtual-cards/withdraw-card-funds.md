# Withdraw Card Funds

Pull funds off an issued virtual card back to your merchant wallet balance.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/vcard-withdraw`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field    | Type            | Required | Description                                  |
| -------- | --------------- | -------- | -------------------------------------------- |
| `cardid` | string          | Yes      | The card's unique ID (`cardid` or `vcardid`) |
| `amount` | string / number | Yes      | Amount to withdraw from the card balance     |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location 'https://api.oneappgo.com/v1/business/vcard-withdraw.php' \
  --header 'Authorization: Bearer YOUR_SECRET_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "cardid": "CARD_12345",
    "amount": "25.00"
  }'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/vcard-withdraw.php', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ cardid: 'CARD_12345', amount: '25.00' })
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Python (Requests)" %}
{% code overflow="wrap" lineNumbers="true" %}
```python
import requests
import json

url = "{{base_url}}/business/vcard-withdraw.php"
payload = json.dumps({'cardid': 'CARD_12345', 'amount': '25.00'})
headers = {
  'Authorization': 'Bearer YOUR_SECRET_KEY',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)
print(response.text)
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Sample Response

{% code title="Sample Response" overflow="wrap" %}
```json
{
  "status": true,
  "responsecode": "01",
  "message": "Virtual Card withdrawal of $25.00 is processing",
  "data": []
}
```
{% endcode %}

### Duplicate Withdrawal Protection

To prevent accidental double charges or duplicate withdrawals:

* If the same business retries the same card withdrawal amount within the configured retry window, the API blocks duplicate charges and returns a normalized `responsecode: "00"` with a duplicate-retry error message instead of creating a second withdrawal.
* **Default Retry Window:** 50 seconds.
* **Business Specific Default:** Business `4629` uses a 120-second retry window unless overridden.
* **Admin Override:** Admins can override `duplicate_window_seconds` per business in the `virtualcard` service pricing/access record.

### Webhook Event Details

A successful card withdrawal triggers an outbound webhook event:

* `event_type`: `type: virtualcard_withdrawal` (normalized as `virtualcard_withdraw`)
* `available_balance`: Represents the card balance after withdrawal.
* `old_balance`: Represents the card balance before withdrawal.
