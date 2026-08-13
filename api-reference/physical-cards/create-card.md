# Create Card

Submit a request for a physical card. Returns a `requestid` to track fulfillment.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/debitcard-issuance`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field             | Type    | Required                            | Description                                                                |
| ----------------- | ------- | ----------------------------------- | -------------------------------------------------------------------------- |
| `customerid`      | string  | Yes                                 | Tracking ID from **Create Customer (Full KYC)**                            |
| `cardtype`        | string  | Yes                                 | `debit` or `credit`                                                        |
| `nin`             | string  | Yes                                 | Customer's NIN                                                             |
| `photocustomised` | boolean | Yes                                 | `true` to print the customer's photo on the card, `false` for a plain card |
| `photo`           | string  | Only if `photocustomised` is `true` | URL of the customer's photo                                                |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/debitcard-issuance' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data-raw '{
    "customerid": "891106211211",
    "cardtype": "debit",
    "nin": "21121212029",
    "photocustomised": false,
    "photo": ""
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/debitcard-issuance', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    customerid: '891106211211',
    cardtype: 'debit',
    nin: '21121212029',
    photocustomised: false,
    photo: ''
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
  "customerid": "891106211211"
  "cardtype": "debit",
  "nin": "21121212029",
  "photocustomised": false,
  "photo": ""
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/debitcard-issuance',
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

url = "{{base_url}}/business/debitcard-issuance"

payload = json.dumps({'customerid': '891106211211', 'cardtype': 'debit', 'nin': '21121212029', 'photocustomised': False, 'photo': ''})
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
  CURLOPT_URL => '{{base_url}}/business/debitcard-issuance',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "customerid": "891106211211",
    "cardtype": "debit",
    "nin": "21121212029",
    "photocustomised": false,
    "photo": ""
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/debitcard-issuance'));
request.body = json.encode({
  "customerid": "891106211211"
  "cardtype": "debit",
  "nin": "21121212029",
  "photocustomised": false,
  "photo": ""
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
  "message": "Card Request Successfully Submitted for John Doe",
  "data": {
    "requestid": "1fc0e17f-31ea-c9ea-0230-770e7c7bf876",
    "customerid": "BLD19661746"
  }
}
```
{% endtab %}

{% tab title="Failure" %}
```json
{
  "status": false,
  "responsecode": "00",
  "message": "Unable to process request. Invalid authorization key",
  "requestid": ""
}
```
{% endtab %}
{% endtabs %}
