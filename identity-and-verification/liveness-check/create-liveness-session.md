# Create Liveness Session

Initiate a new face-liveness session for an existing customer. The customer must already have a KYC record before you can run this check.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/create-face-liveness-session`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field                 | Type   | Required | Description                                                                                             |
| --------------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------- |
| `customer_trackingid` | string | Yes      | The business customer's tracking ID (preferred field — `trackid` and legacy `userid` are also accepted) |
| `purpose`             | string | Yes      | Reason for the check, e.g. `business_verification`                                                      |
| `challenge_type`      | string | Yes      | e.g. `FaceMovementAndLightChallenge`                                                                    |
| `bridge_origin`       | string | Yes      | Your app's origin, for the liveness bridge                                                              |
| `bridge_url`          | string | Yes      | Your app's liveness callback UI URL                                                                     |

{% hint style="info" %}
Keep your secret key on your server only — never expose it in front-end code.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/create-face-liveness-session' --header 'Authorization: Bearer YOUR_SECRET_KEY' --header 'Content-Type: application/json' --data '{
    "customer_trackingid": "BLD123456789",
    "purpose": "business_verification",
    "challenge_type": "FaceMovementAndLightChallenge",
    "bridge_origin": "https://your-app.example.com",
    "bridge_url": "https://your-app.example.com/liveness/"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/create-face-liveness-session', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    customer_trackingid: 'BLD123456789',
    purpose: 'business_verification',
    challenge_type: 'FaceMovementAndLightChallenge',
    bridge_origin: 'https://your-app.example.com',
    bridge_url: 'https://your-app.example.com/liveness/'
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
    "customer_trackingid": "BLD123456789",
    "purpose": "business_verification",
    "challenge_type": "FaceMovementAndLightChallenge",
    "bridge_origin": "https://your-app.example.com",
    "bridge_url": "https://your-app.example.com/liveness/"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/create-face-liveness-session',
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

url = "{{base_url}}/business/create-face-liveness-session"

payload = json.dumps({'customer_trackingid': 'BLD123456789', 'purpose': 'business_verification', 'challenge_type': 'FaceMovementAndLightChallenge', 'bridge_origin': 'https://your-app.example.com', 'bridge_url': 'https://your-app.example.com/liveness/'})
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
  CURLOPT_URL => '{{base_url}}/business/create-face-liveness-session',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "customer_trackingid": "BLD123456789",
    "purpose": "business_verification",
    "challenge_type": "FaceMovementAndLightChallenge",
    "bridge_origin": "https://your-app.example.com",
    "bridge_url": "https://your-app.example.com/liveness/"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/create-face-liveness-session'));
request.body = json.encode({'customer_trackingid': 'BLD123456789', 'purpose': 'business_verification', 'challenge_type': 'FaceMovementAndLightChallenge', 'bridge_origin': 'https://your-app.example.com', 'bridge_url': 'https://your-app.example.com/liveness/'});
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

**Response Fields:**

* `session_id`: Unique session tracking code.
* `bridge_url`: Web link for the user to complete the challenge.
* `liveness_fee`: Charge billed for the check.

Once you have a session, open the returned `bridge_url` (or your own `/liveness/` UI) to let the customer complete the check.
