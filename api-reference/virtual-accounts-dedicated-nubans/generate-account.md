# Generate Account

Create a dedicated virtual NUBAN for a customer. Payments into this account land directly in your Boldd Wallet.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/dedicated-account`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field        | Type   | Required | Description                                                      |
| ------------ | ------ | -------- | ---------------------------------------------------------------- |
| `trackingid` | string | Yes      | A unique ID you generate for this user                           |
| `firstname`  | string | Yes      | User's first name                                                |
| `lastname`   | string | Yes      | User's last name                                                 |
| `userbvn`    | string | Yes      | User's BVN                                                       |
| `useremail`  | string | Yes      | User's email                                                     |
| `userphone`  | string | Yes      | User's phone number                                              |
| `bankcode`   | string | No       | Overrides your **Setup Preferred Bank** default for this account |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/dedicated-account' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "trackingid": "2727",
    "firstname": "John",
    "lastname": "Doe",
    "userbvn": "22222253444",
    "useremail": "johndoe@example.com",
    "userphone": "09123456789",
    "bankcode": "120001"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/dedicated-account', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    trackingid: '2727',
    firstname: 'John',
    lastname: 'Doe',
    userbvn: '22222253444',
    useremail: 'johndoe@example.com',
    userphone: '09123456789',
    bankcode: '120001'
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
    "trackingid": "2727",
    "firstname": "John",
    "lastname": "Doe",
    "userbvn": "22222253444",
    "useremail": "johndoe@example.com",
    "userphone": "09123456789",
    "bankcode": "120001"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/dedicated-account',
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

url = "{{base_url}}/dedicated-account"

payload = json.dumps({'trackingid': '2727', 'firstname': 'John', 'lastname': 'Doe', 'userbvn': '22222253444', 'useremail': 'johndoe@example.com', 'userphone': '09123456789', 'bankcode': '120001'})
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
  CURLOPT_URL => '{{base_url}}/dedicated-account',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "trackingid": "2727",
    "firstname": "John",
    "lastname": "Doe",
    "userbvn": "22222253444",
    "useremail": "johndoe@example.com",
    "userphone": "09123456789",
    "bankcode": "120001"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/dedicated-account'));
request.body = json.encode({'trackingid': '2727', 'firstname': 'John', 'lastname': 'Doe', 'userbvn': '22222253444', 'useremail': 'johndoe@example.com', 'userphone': '09123456789', 'bankcode': '120001'});
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
  "message": "Account Number Successfully Generated",
  "trackingref": "001858002",
  "trackingid": "002",
  "acctname": "John Doe",
  "acctno": "3984124113",
  "clientid": "1858000",
  "bankcode": "120001",
  "bankname": "9 PAYMENT SERVICE BANK"
}
```
{% endcode %}
