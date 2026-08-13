# Payment Status

Check a transaction's delivery/settlement status - the recommended way to confirm what happened to a transfer or payment before deciding whether to retry.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/checktrans-status`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field       | Type   | Required | Description                                                                    |
| ----------- | ------ | -------- | ------------------------------------------------------------------------------ |
| `reference` | string | Yes      | Transaction reference returned by Boldd, or your own merchant-passed reference |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/checktrans-status' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "reference": "CHK486870908B7468378171"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/checktrans-status', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ reference: 'CHK486870908B7468378171' })
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
    "reference": "CHK486870908B7468378171"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/checktrans-status',
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

url = "{{base_url}}/checktrans-status"

payload = json.dumps({'reference': 'CHK486870908B7468378171'})
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
  CURLOPT_URL => '{{base_url}}/checktrans-status',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "reference": "CHK486870908B7468378171"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/checktrans-status'));
request.body = json.encode({'reference': 'CHK486870908B7468378171'});
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

#### Sample response 200

{% code title="Sample response  200" overflow="wrap" %}
```json
{
  "status": true,
  "message": "Transaction Retrieved",
  "deliveryStatus": "Successful",
  "responseCode": "01",
  "payRef": "API1725870632SM517",
  "paymentTime": "09 Sep 2024 09:30 am",
  "recipient": "002317660",
  "amount": "50000.00",
  "product": "sendmoney",
  "prevBalance": "1050000.00",
  "newBalance": "1000000.00",
  "fee": "20.00",
  "totalCharged": "50020.00",
  "provRef": "54adfb6ebadb6764a6f07",
  "currency": "NGN",
  "accountName": "ADEAYO",
  "accountNo": "002317660",
  "bankName": "Access Bank",
  "bankCode": "063",
  "narration": "transfer",
  "paytype": "DEBIT"
}
```
{% endcode %}

#### Sample response 400

{% code title="Sample response  400" overflow="wrap" %}
```json
{
  "status": false,
  "message": "Invalid request"
}
```
{% endcode %}

{% hint style="info" %}
`product` in the response tells you which service the transaction belongs to (e.g. `sendmoney`), so a single status endpoint can be used across payment types.
{% endhint %}
