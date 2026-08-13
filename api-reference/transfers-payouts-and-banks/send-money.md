# Send Money

Transfer funds to any registered financial institution in Nigeria. Requires the `sendmoney` service grant (see **Service Access & Limits**).

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/sendmoney`

**Request Headers**

<table><thead><tr><th width="157.66668701171875">Header</th><th width="95.99993896484375">Type</th><th width="111">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>Authorization</code></td><td><code>String</code></td><td>Yes</td><td>Bearer token authentication (e.g. <code>Bearer YOUR_SECRET_KEY</code>).</td></tr><tr><td><code>Content-Type</code></td><td><code>String</code></td><td>Yes</td><td>Request body format (e.g. <code>application/json</code>).</td></tr></tbody></table>

#### Request Body

| Field       | Type   | Required | Description                               |
| ----------- | ------ | -------- | ----------------------------------------- |
| `amount`    | string | Yes      | Amount to transfer                        |
| `accountno` | string | Yes      | Destination account number                |
| `acctname`  | string | Yes      | Destination account holder name           |
| `bankcode`  | string | Yes      | Destination bank code — see **Bank List** |
| `bankname`  | string | Yes      | Destination bank name                     |
| `reference` | string | Yes      | Your unique transaction reference         |
| `currency`  | string | No       | `NGN`, `GHS`, `ZAR`, or `USD`             |
| `narration` | string | No       | Reason for the transfer                   |

{% hint style="info" %}
You only need to send one of `bankcode` or `bankname`  -  the API normalizes the missing one where possible. If a placeholder or unresolvable bank name is sent, you still get a safe JSON error rather than a blank payload.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request POST '{{base_url}}/sendmoney' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "amount": "100000",
    "bankcode": "000013",
    "bankname": "GT BANK",
    "accountno": "0245000000",
    "acctname": "Olajide Olajide",
    "reference": "shudgyutg876542",
    "narration": "Transfer to my client",
    "currency": "NGN"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/sendmoney', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    amount: '100000',
    bankcode: '000013',
    bankname: 'GT BANK',
    accountno: '0245000000',
    acctname: 'Olajide Olajide',
    reference: 'shudgyutg876542',
    narration: 'Transfer to my client',
    currency: 'NGN'
  })
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Node.js (Axios)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
    "amount": "100000",
    "bankcode": "000013",
    "bankname": "GT BANK",
    "accountno": "0245000000",
    "acctname": "Olajide Olajide",
    "reference": "shudgyutg876542",
    "narration": "Transfer to my client",
    "currency": "NGN"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/sendmoney',
  headers: { 
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  data : data
};

axios.request(config)
.then((response) => {
  console.log(JSON.stringify(response.data));
})
.catch((error) => {
  console.log(error);
});
```
{% endcode %}
{% endtab %}

{% tab title="Python (Requests)" %}
{% code overflow="wrap" lineNumbers="true" %}
```python
import requests
import json

url = "{{base_url}}/sendmoney"

payload = json.dumps({'amount': '100000', 'bankcode': '000013', 'bankname': 'GT BANK', 'accountno': '0245000000', 'acctname': 'Olajide Olajide', 'reference': 'shudgyutg876542', 'narration': 'Transfer to my client', 'currency': 'NGN'})
headers = {
  'Authorization': 'Bearer YOUR_SECRET_KEY',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}
{% endtab %}

{% tab title="PHP (cURL)" %}
{% code overflow="wrap" lineNumbers="true" %}
```php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => '{{base_url}}/sendmoney',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "amount": "100000",
    "bankcode": "000013",
    "bankname": "GT BANK",
    "accountno": "0245000000",
    "acctname": "Olajide Olajide",
    "reference": "shudgyutg876542",
    "narration": "Transfer to my client",
    "currency": "NGN"
}',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer YOUR_SECRET_KEY',
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```
{% endcode %}
{% endtab %}

{% tab title="Dart" %}
{% code overflow="wrap" lineNumbers="true" %}
```dart
var headers = {
  'Authorization': 'Bearer YOUR_SECRET_KEY',
  'Content-Type': 'application/json'
};
var request = http.Request('POST', Uri.parse('{{base_url}}/sendmoney'));
request.body = json.encode({'amount': '100000', 'bankcode': '000013', 'bankname': 'GT BANK', 'accountno': '0245000000', 'acctname': 'Olajide Olajide', 'reference': 'shudgyutg876542', 'narration': 'Transfer to my client', 'currency': 'NGN'});
request.headers.addAll(headers);

http.StreamedResponse response = await request.send();

if (response.statusCode == 200) {
  print(await response.stream.bytesToString());
}
else {
  print(response.reasonPhrase);
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Sample response

{% code title="Sample response" overflow="wrap" %}
```json
{
  "status": true,
  "message": "Transfer Successfully Completed",
  "txref": "API365022038SM347",
  "charged": 100000,
  "newbal": 600023.80
}
```
{% endcode %}

{% hint style="info" %}
If your business doesn't have `sendmoney` access, the API returns a safe failure response -  it will not silently succeed or return an empty payload.
{% endhint %}
