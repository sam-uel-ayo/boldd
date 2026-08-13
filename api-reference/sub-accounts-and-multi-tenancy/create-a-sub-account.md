# Create a Sub-Account

Sub-accounts represent **business entities under your parent Boldd account** - useful if you run a marketplace or platform and need to onboard your own merchants, each with an isolated balance. This is distinct from **Customers** (Identity & Verification), which represent KYC-verified end users.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/create-subaccount`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field         | Type    | Required | Description                                                                      |
| ------------- | ------- | -------- | -------------------------------------------------------------------------------- |
| `firstname`   | string  | Yes      | Sub-account holder's first name                                                  |
| `lastname`    | string  | Yes      | Sub-account holder's last name                                                   |
| `email`       | string  | Yes      | Sub-account holder's email                                                       |
| `phoneno`     | string  | Yes      | Sub-account holder's phone number                                                |
| `loginaccess` | boolean | No       | Pass `true` to give this sub-account dashboard login access. Defaults to `false` |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/create-subaccount' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data-raw '{
    "phoneno": "09000000001",
    "firstname": "Olaope",
    "lastname": "James",
    "email": "johndoe@example.com",
    "loginaccess": false
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/create-subaccount', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    phoneno: '09000000001',
    firstname: 'Olaope',
    lastname: 'James',
    email: 'johndoe@example.com',
    loginaccess: false
  })
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Node.js (Axios)" %}
{% code overflow="wrap" lineNumbers="true" %}
```json
const axios = require('axios');
let data = JSON.stringify({
  "phoneno": "09000000001",
  "firstname": "Olaope",
  "lastname": "James",
  "email": "johndoe@exaple.com",
  "loginaccess": false
});

let config = {
  method: 'post',
  url: '{{base_url}}/business/create-subaccount',
  headers: { 
    'Content-Type': 'application/json', 
    'Authorization': 'Bearer YOUR_SECRET_KEY', 
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

url = "{{base_url}}/business/create-subaccount"

payload = json.dumps({'phoneno': '09000000001', 'firstname': 'Olaope', 'lastname': 'James', 'email': 'johndoe@example.com', 'loginaccess': False})
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer YOUR_SECRET_KEY'
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
  CURLOPT_URL => '{{base_url}}/business/create-subaccount',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "phoneno": "09000000001",
    "firstname": "Olaope",
    "lastname": "James",
    "email": "johndoe@example.com",
    "loginaccess": false
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json',
    'Authorization: Bearer YOUR_SECRET_KEY'
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
  'Content-Type': 'application/json',
  'Authorization': 'Bearer YOUR_SECRET_KEY'
};
var request = http.Request('POST', Uri.parse('{{base_url}}/business/create-subaccount'));
request.body = json.encode({'phoneno': '09000000001', 'firstname': 'Olaope', 'lastname': 'James', 'email': 'johndoe@example.com', 'loginaccess': False});
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
  "message": "Sub Account Successfully Created For Olaope James",
  "trackingid": "00104K0000000"
}
```
{% endcode %}

Keep the returned `trackingid` - every other sub-account action (attaching banks, checking history, checking wallet) is keyed off it.
