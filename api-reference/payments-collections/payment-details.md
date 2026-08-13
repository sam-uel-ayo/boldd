# Payment Details

Fetch full details of a single transaction by reference.

**Endpoint**

<mark style="color:blue;">`GET`</mark> `{{base_url}}/business/fetchtrans`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |

#### Query Parameters

| Field       | Type   | Required | Description               |
| ----------- | ------ | -------- | ------------------------- |
| `reference` | string | Yes      | The transaction reference |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET '{{base_url}}/business/fetchtrans?reference=63490b1643370903287' \
--header 'Authorization: Bearer YOUR_SECRET_KEY'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/fetchtrans?reference=63490b1643370903287', {
  headers: { 'Authorization': 'Bearer YOUR_SECRET_KEY' }
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Node.js (Axios)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({{base_url}});

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/fetchtrans?reference=63490b1643370903287',
  headers: { 
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

url = "{{base_url}}/business/fetchtrans?reference=63490b1643370903287"

payload = '{{base_url}}'
headers = {
  'Authorization': 'Bearer YOUR_SECRET_KEY'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}
{% endtab %}

{% tab title="PHP (cURL)" %}
{% code overflow="wrap" lineNumbers="true" %}
```php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => '{{base_url}}/business/fetchtrans?reference=63490b1643370903287',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_POSTFIELDS =>'{{base_url}}',
  CURLOPT_HTTPHEADER => array(
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
  'Authorization': 'Bearer YOUR_SECRET_KEY'
};
var request = http.Request('GET', Uri.parse('{{base_url}}/business/fetchtrans?reference=63490b1643370903287'));
request.body = '{{base_url}}';
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
  "message": "Successful",
  "transtatus": "Completed",
  "transid": "1000865",
  "amount": "300.00",
  "amount_settled": "292.80",
  "transfee": "7.20",
  "prevbal": "5118.75",
  "newbal": "5411.55",
  "currency": "NGN",
  "reference": "63490b1643370903287",
  "customer_reference": "2910_1643370902",
  "transaction_token": "cfda35a0d3a970fd47c57eda6c230ba1",
  "customer_email": "example@gmail.com",
  "customer_phone": "",
  "payment_channel": "rave",
  "paid_through": "api",
  "mode": "test",
  "attempt": 1,
  "payment_time": "28, Fri. Jan. 2022",
  "gateway": "Flutterwave",
  "statustext": "Completed",
  "time_elapsed": "00:58"
}
```
{% endcode %}
