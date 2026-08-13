# Liveness Callback

Boldd sends the final face liveness result asynchronously to your configured `callback_url` once the customer completes the bridge challenge.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/liveness-callback`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

### Webhook Body Fields

| Field                 | Description                             |
| --------------------- | --------------------------------------- |
| `session_id`          | The session this result belongs to      |
| `customer_trackingid` | The customer being verified             |
| `status`              | Result of liveness test, e.g. `success` |
| `similarity`          | Match confidence score percentage       |
| `challenge_type`      | The challenge type used                 |

{% hint style="info" %}
Before showing the liveness UI or configuring bridge settings, check your business profile's `has_liveness_access` field to confirm access is active.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/liveness-callback' --header 'Authorization: Bearer YOUR_SECRET_KEY' --header 'Content-Type: application/json' --data '{
    "session_id": "LIV_987654321",
    "customer_trackingid": "BLD123456789",
    "status": "success",
    "similarity": 98.4,
    "challenge_type": "FaceMovementAndLightChallenge"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/liveness-callback', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    session_id: 'LIV_987654321',
    customer_trackingid: 'BLD123456789',
    status: 'success',
    similarity: 98.4,
    challenge_type: 'FaceMovementAndLightChallenge'
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
    "session_id": "LIV_987654321",
    "customer_trackingid": "BLD123456789",
    "status": "success",
    "similarity": 98.4,
    "challenge_type": "FaceMovementAndLightChallenge"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/liveness-callback',
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

url = "{{base_url}}/business/liveness-callback"

payload = json.dumps({'session_id': 'LIV_987654321', 'customer_trackingid': 'BLD123456789', 'status': 'success', 'similarity': 98.4, 'challenge_type': 'FaceMovementAndLightChallenge'})
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
  CURLOPT_URL => '{{base_url}}/business/liveness-callback',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "session_id": "LIV_987654321",
    "customer_trackingid": "BLD123456789",
    "status": "success",
    "similarity": 98.4,
    "challenge_type": "FaceMovementAndLightChallenge"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/liveness-callback'));
request.body = json.encode({'session_id': 'LIV_987654321', 'customer_trackingid': 'BLD123456789', 'status': 'success', 'similarity': 98.4, 'challenge_type': 'FaceMovementAndLightChallenge'});
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
