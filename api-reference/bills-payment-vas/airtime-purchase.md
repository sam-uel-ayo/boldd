# Airtime Purchase

Sell mobile airtime directly from any Nigerian network.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/airtime`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

### Network IDs

| Network | `network_id` |
| ------- | ------------ |
| GLO     | `1`          |
| MTN     | `2`          |
| AIRTEL  | `3`          |
| 9MOBILE | `4`          |

#### Request Body

| Field        | Type   | Required | Description                   |
| ------------ | ------ | -------- | ----------------------------- |
| `phoneno`    | string | Yes      | Recipient phone number        |
| `network_id` | string | Yes      | See table above               |
| `amount`     | string | Yes      | Amount of airtime to purchase |
| `reference`  | string | No       | Your transaction reference    |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request POST '{{base_url}}/airtime' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "phoneno": "07012345678",
    "network_id": "2",
    "amount": "5000",
    "reference": "O4I3U8SRNYOIYT"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/airtime', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ phoneno: '07012345678', network_id: '2', amount: '5000', reference: 'O4I3U8SRNYOIYT' })
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
    "phoneno": "07012345678",
    "network_id": "2",
    "amount": "5000",
    "reference": "O4I3U8SRNYOIYT"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/airtime',
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

url = "{{base_url}}/airtime"

payload = json.dumps({'phoneno': '07012345678', 'network_id': '2', 'amount': '5000', 'reference': 'O4I3U8SRNYOIYT'})
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
  CURLOPT_URL => '{{base_url}}/airtime',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "phoneno": "07012345678",
    "network_id": "2",
    "amount": "5000",
    "reference": "O4I3U8SRNYOIYT"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/airtime'));
request.body = json.encode({'phoneno': '07012345678', 'network_id': '2', 'amount': '5000', 'reference': 'O4I3U8SRNYOIYT'});
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
  "txref": "API665023309a400",
  "charged": 4900.5,
  "newbal": 570004.3
}
```
{% endcode %}
