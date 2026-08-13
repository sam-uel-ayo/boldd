# Attach Payout Account

Attach a bank account that this sub-account can withdraw/settle to.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/addpayoutbank`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field        | Type   | Required | Description                          |
| ------------ | ------ | -------- | ------------------------------------ |
| `trackingid` | string | Yes      | Sub-account tracking ID              |
| `bankcode`   | string | Yes      | Payout bank code — see **Bank List** |
| `bankname`   | string | Yes      | Payout bank name                     |
| `accountno`  | string | Yes      | Payout account number                |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/addpayoutbank' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data-raw '{
    "trackingid": "00104K0000000",
    "bankname": "GT Bank",
    "bankcode": "000013",
    "accountno": "0212222223"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/addpayoutbank', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    trackingid: '00104K0000000',
    bankname: 'GT Bank',
    bankcode: '000013',
    accountno: '0212222223'
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
  "trackingid":"00104K0000000",
  "bankname":"GT Bank",
  "bankcode":  "00013",
  "accountno": "0212222223"
});

let config = {
  method: 'post',
  url: '{{base_url}}/business/addpayoutbank',
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

url = "{{base_url}}/business/addpayoutbank"

payload = json.dumps({'trackingid': '00104K0000000', 'bankname': 'GT Bank', 'bankcode': '000013', 'accountno': '0212222223'})
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
  CURLOPT_URL => '{{base_url}}/business/addpayoutbank',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "trackingid": "00104K0000000",
    "bankname": "GT Bank",
    "bankcode": "000013",
    "accountno": "0212222223"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/addpayoutbank'));
request.body = json.encode({'trackingid': '00104K0000000', 'bankname': 'GT Bank', 'bankcode': '000013', 'accountno': '0212222223'});
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
  "message": "Payout Account Successfully Added",
  "trackingid": "00104K0000000"
}
```
{% endcode %}
