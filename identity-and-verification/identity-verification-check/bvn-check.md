# BVN Check

Verify a customer's Bank Verification Number (BVN) against official banking registry records. This check is available in Basic and Premium modes.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/bvnkyc`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field         | Type   | Required | Description          |
| ------------- | ------ | -------- | -------------------- |
| `bvnno`       | string | Yes      | 11-digit BVN number  |
| `verify_type` | string | Yes      | `basic` or `premium` |

{% hint style="info" %}
Keep your secret key on your server only - never expose it in front-end code.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/bvnkyc' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "verify_type": "premium",
    "bvnno": "22636318272"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/bvnkyc', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ verify_type: 'premium', bvnno: '22636318272' })
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
    "verify_type": "premium",
    "bvnno": "22636318272"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/bvnkyc',
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

url = "{{base_url}}/bvnkyc"

payload = json.dumps({'verify_type': 'premium', 'bvnno': '22636318272'})
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
  CURLOPT_URL => '{{base_url}}/bvnkyc',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "verify_type": "premium",
    "bvnno": "22636318272"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/bvnkyc'));
request.body = json.encode({'verify_type': 'premium', 'bvnno': '22636318272'});
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

#### Sample Response

{% code title="Sample Response" overflow="wrap" %}
```json
{
  "status": true,
  "responseCode": "01",
  "msg": "Verified",
  "data": {
    "title": "Mr",
    "fullname": "AMAD JOHN CKUKWU",
    "customeremail": "",
    "gender": "male",
    "dob": "01-02-1956",
    "phone_number": "09012345678",
    "alternate_phoneno": "08012345678",
    "residence": "Yola State",
    "address": "2, Iwajowa street, Agugu",
    "country": "nigeria",
    "level_of_account": "Level 3 - High Level Accounts",
    "watchlisted": false,
    "photo": "BASE64 ENCODED"
  }
}
```
{% endcode %}
