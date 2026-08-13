# Sub-Accounts History

Get the transaction/ledger history for a specific sub-account.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/subaccount-history`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field        | Type   | Required | Description             |
| ------------ | ------ | -------- | ----------------------- |
| `trackingid` | string | Yes      | Sub-account tracking ID |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/subaccount-history' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "trackingid": "bi158338"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/subaccount-history', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ trackingid: 'bi158338' })
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Node.js (Axios)" %}
{% code overflow="wrap" lineNumbers="true" %}
```json
const axios = require('axios');

let config = {
  method: 'post',
  url: '{{base_url}}/business/subaccount-history',
  headers: { 
    'Authorization': 'Bearer YOUR_SECRET_KEY',
  }
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

url = "{{base_url}}/business/subaccount-history"

payload = json.dumps({'trackingid': 'bi158338'})
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
  CURLOPT_URL => '{{base_url}}/business/subaccount-history',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "trackingid": "bi158338"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/subaccount-history'));
request.body = json.encode({'trackingid': 'bi158338'});
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
  "message": "Transaction history found.",
  "data": [
    {
      "prevbal": "0.00",
      "newbal": "250002.00",
      "descriptions": "Fund credit to Olajide Olatunji subaccount",
      "type": "credit",
      "reference": "BW1S405671B8165007",
      "paidtru": "boldd",
      "status": "1",
      "trackingid": "bi158338",
      "date_created": "16, January 2024 11:39 am",
      "amount": "250002.00",
      "paystatus": "Completed"
    }
  ]
}
```
{% endcode %}
