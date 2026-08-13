# Create Customer (Tier 1)

Tier 1 is a lightweight KYC level - enough to transact at a basic level without full identity document upload. Use **Full KYC** (next page) when a customer needs virtual cards, physical cards, or global accounts.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/create-tier1`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field           | Type   | Required | Description                                       |
| --------------- | ------ | -------- | ------------------------------------------------- |
| `first_name`    | string | Yes      | Customer first name                               |
| `last_name`     | string | Yes      | Customer last name                                |
| `email_address` | string | Yes      | Customer email                                    |
| `phone_number`  | string | Yes      | Customer mobile number                            |
| `birth_date`    | string | Yes      | Format `yyyy-mm-dd`. Customer must be at least 18 |
| `nationality`   | string | Yes      | e.g. `Nigeria`                                    |

{% hint style="info" %}
Keep your secret key on your server only - never expose it in front-end code.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/create-tier1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data-raw '{
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "07012345678",
    "birth_date": "2000-03-23",
    "nationality": "Nigeria",
    "email_address": "email@example.com"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/create-tier1', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    first_name: 'John',
    last_name: 'Doe',
    phone_number: '07012345678',
    birth_date: '2000-03-23',
    nationality: 'Nigeria',
    email_address: 'email@example.com'
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
  "first_name": "John",
  "last_name": "Doe",
  "phone_number": "07012345678",
  "birth_date": "2000-03-23",
  "natioanality": "Nigeria",
  "email_address": "email@example.com"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/create-tier1',
  headers: { 
    'Content-Type': 'application/json', 
    'Authorization': 'Bearer YOUR_SECRET_KEY' 
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

url = "{{base_url}}/business/create-tier1"

payload = json.dumps({'first_name': 'John', 'last_name': 'Doe', 'phone_number': '07012345678', 'birth_date': '2000-03-23', 'nationality': 'Nigeria', 'email_address': 'email@example.com'})
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
  CURLOPT_URL => '{{base_url}}/business/create-tier1',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "07012345678",
    "birth_date": "2000-03-23",
    "nationality": "Nigeria",
    "email_address": "email@example.com"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/create-tier1'));
request.body = json.encode({
  "first_name": "John",
  "last_name": "Doe",
  "phone_number": "07012345678",
  "birth_date": "2000-03-23",
  "natioanality": "Nigeria",
  "email_address": "email@example.com"
});
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

{% tabs %}
{% tab title="Success" %}
```json
{
  "status": true,
  "responsecode": "01",
  "message": "Tier 1 account successfully created for John Doe",
  "trackid": "06211211"
}
```
{% endtab %}

{% tab title="Failure" %}
```json
{
  "status": false,
  "responsecode": "00",
  "message": "Unable to process request. Invalid authorization key",
  "trackid": ""
}
```
{% endtab %}
{% endtabs %}

Keep the returned `trackid` — you'll need it for virtual accounts, cards, and other customer-linked actions.
