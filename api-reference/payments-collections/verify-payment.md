# Verify Payment

Confirm the actual outcome of a transaction. Always call this server-side after Initialize Payment or Inline Checkout - never trust a client-side redirect or callback alone.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/verifytrans`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field       | Type   | Required | Description                         |
| ----------- | ------ | -------- | ----------------------------------- |
| `reference` | string | Yes      | The transaction reference to verify |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request POST '{{base_url}}/business/verifytrans' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "reference": "634967hg599287"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/verifytrans', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ reference: '634967hg599287' })
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
    "reference": "634967hg599287"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/verifytrans',
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

url = "{{base_url}}/business/verifytrans"

payload = json.dumps({'reference': '634967hg599287'})
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
  CURLOPT_URL => '{{base_url}}/business/verifytrans',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "reference": "634967hg599287"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/verifytrans'));
request.body = json.encode({'reference': '634967hg599287'});
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
  "message": "Successful",
  "reference": "63490b1f59287",
  "data": {
    "responsecode": "01",
    "trans_status": "Successful",
    "amount": "150000.00",
    "charged_amount": "150000.00",
    "amount_settled": "150000.00",
    "fee": "0.00",
    "mode": "live environment",
    "env": "live",
    "payment_timestamp": "1694387652",
    "currency": "NGN",
    "reference": "63490b1f59287",
    "customer_reference": "2913_1643371498",
    "transaction_token": "c31f54f3b7986a92d04d1699f51227b3",
    "customer_email": "test@gmail.com",
    "customer_name": "",
    "payment_channel": "paystack",
    "paid_through": "api",
    "payment_time": "28 Jan 2022 01:04"
  }
}
```
{% endcode %}

#### Dynamic Transfer Confirmation & Reconciliation

When verifying dynamic transfer payments, the response distinguishes exact payment, underpayment, and overpayment:

* **Clean Success (`responsecode: "01"`, `status: true`):** Paid exact amount (`payment_completion: "completed"`).
* **Underpaid (`responsecode: "02"`, `status: false`, `payment_status: true`):** Customer sent less than expected (`payment_completion: "underpaid"`, `reconciliation_required: "1"`). Inspect `amount_difference` and `amount_paid`.
* **Overpaid (`responsecode: "03"`, `status: false`, `payment_status: true`):** Customer sent more than expected (`payment_completion: "overpaid"`, `reconciliation_required: "1"`). Inspect `amount_difference` and `amount_paid`.
* **Pending (`responsecode: "00"`, `status: false`, `payment_status: false`):** Awaiting customer payment (`payment_completion: "pending"`).
