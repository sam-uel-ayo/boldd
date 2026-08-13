# Cable TV Purchase

Purchase/renew a cable TV subscription for a verified decoder.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/cabletv`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field       | Type   | Required | Description                             |
| ----------- | ------ | -------- | --------------------------------------- |
| `tvno`      | string | Yes      | Decoder IUC number                      |
| `tv`        | string | Yes      | `DSTV`, `GOTV`, or `STARTIMES`          |
| `amount`    | string | Yes      | Package amount — from **Cable TV List** |
| `custname`  | string | Yes      | From **Verify IUC** response            |
| `custno`    | string | Yes      | From **Verify IUC** response            |
| `reference` | string | No       | Your transaction reference              |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request POST '{{base_url}}/cabletv' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "tvno": "7528393100",
    "tv": "GOTV",
    "custname": "IBRAHIM MARY OPE",
    "custno": "376946518",
    "amount": "5000",
    "reference": "OI8UYTEFYDTYTG7"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/cabletv', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ tvno: '7528393100', tv: 'GOTV', custname: 'IBRAHIM MARY OPE', custno: '376946518', amount: '5000', reference: 'OI8UYTEFYDTYTG7' })
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
    "tvno": "7528393100",
    "tv": "GOTV",
    "custname": "IBRAHIM MARY OPE",
    "custno": "376946518",
    "amount": "5000",
    "reference": "OI8UYTEFYDTYTG7"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/cabletv',
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

url = "{{base_url}}/cabletv"

payload = json.dumps({'tvno': '7528393100', 'tv': 'GOTV', 'custname': 'IBRAHIM MARY OPE', 'custno': '376946518', 'amount': '5000', 'reference': 'OI8UYTEFYDTYTG7'})
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
  CURLOPT_URL => '{{base_url}}/cabletv',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "tvno": "7528393100",
    "tv": "GOTV",
    "custname": "IBRAHIM MARY OPE",
    "custno": "376946518",
    "amount": "5000",
    "reference": "OI8UYTEFYDTYTG7"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/cabletv'));
request.body = json.encode({'tvno': '7528393100', 'tv': 'GOTV', 'custname': 'IBRAHIM MARY OPE', 'custno': '376946518', 'amount': '5000', 'reference': 'OI8UYTEFYDTYTG7'});
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
  "message": "Success",
  "txref": "API8650294032c698",
  "charged": 5030,
  "newbal": 100064.8
}
```
{% endcode %}
