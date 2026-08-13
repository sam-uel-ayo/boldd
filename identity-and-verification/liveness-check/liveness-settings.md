# Liveness Settings

Save the default bridge origins, callback URLs, and status settings your business wants to use for face liveness challenges.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/liveness-settings`)

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field           | Type    | Required | Description                                |
| --------------- | ------- | -------- | ------------------------------------------ |
| `bridge_origin` | string  | Yes      | Your app's default origin                  |
| `bridge_url`    | string  | Yes      | Your liveness UI URL                       |
| `callback_url`  | string  | Yes      | Where Boldd sends the final result webhook |
| `status`        | integer | Yes      | Enable/disable status (`1` for active)     |

{% hint style="info" %}
If you send only one of `bridge_origin`, `bridge_url`, or `callback_url`, your other previously saved values are preserved — you don't need to resend all three every time.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/liveness-settings' --header 'Authorization: Bearer YOUR_SECRET_KEY' --header 'Content-Type: application/json' --data '{
    "bridge_origin": "https://your-app.example.com",
    "bridge_url": "https://your-app.example.com/liveness/",
    "callback_url": "https://your-app.example.com/api/liveness/callback",
    "status": 1
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/liveness-settings', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    bridge_origin: 'https://your-app.example.com',
    bridge_url: 'https://your-app.example.com/liveness/',
    callback_url: 'https://your-app.example.com/api/liveness/callback',
    status: 1
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
    "bridge_origin": "https://your-app.example.com",
    "bridge_url": "https://your-app.example.com/liveness/",
    "callback_url": "https://your-app.example.com/api/liveness/callback",
    "status": 1
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/liveness-settings',
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

url = "{{base_url}}/business/liveness-settings"

payload = json.dumps({'bridge_origin': 'https://your-app.example.com', 'bridge_url': 'https://your-app.example.com/liveness/', 'callback_url': 'https://your-app.example.com/api/liveness/callback', 'status': 1})
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
  CURLOPT_URL => '{{base_url}}/business/liveness-settings',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "bridge_origin": "https://your-app.example.com",
    "bridge_url": "https://your-app.example.com/liveness/",
    "callback_url": "https://your-app.example.com/api/liveness/callback",
    "status": 1
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/liveness-settings'));
request.body = json.encode({'bridge_origin': 'https://your-app.example.com', 'bridge_url': 'https://your-app.example.com/liveness/', 'callback_url': 'https://your-app.example.com/api/liveness/callback', 'status': 1});
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
