# Validate Account Name

Resolve an account number and bank code to the account holder's name - use this before Send Money to confirm you're paying the right person.

**Endpoint**

<mark style="color:blue;">`GET`</mark> `{{base_url}}/validate-acctname`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_PUBLIC_KEY`). |

#### Query Parameters

| Field      | Type   | Required | Description                  |
| ---------- | ------ | -------- | ---------------------------- |
| `acctno`   | string | Yes      | Bank account number          |
| `bankcode` | string | Yes      | Bank code from **Bank List** |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET '{{base_url}}/validate-acctname?acctno=0123456789&bankcode=000013' \
--header 'Authorization: Bearer YOUR_PUBLIC_KEY'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/validate-acctname?acctno=0123456789&bankcode=000013', {
  headers: { 'Authorization': 'Bearer YOUR_PUBLIC_KEY' }
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
  url: '{{base_url}}/validate-acctname?acctno=0123456789&bankcode=000013',
  headers: { 
    'Authorization': 'Bearer YOUR_PUBLIC_KEY'
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

url = "{{base_url}}/validate-acctname?acctno=0123456789&bankcode=000013"

payload = '{{base_url}}'
headers = {
  'Authorization': 'Bearer YOUR_PUBLIC_KEY'
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
  CURLOPT_URL => '{{base_url}}/validate-acctname?acctno=0123456789&bankcode=000013',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_POSTFIELDS =>'{{base_url}}',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer YOUR_PUBLIC_KEY'
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
  'Authorization': 'Bearer YOUR_PUBLIC_KEY'
};
var request = http.Request('GET', Uri.parse('{{base_url}}/validate-acctname?acctno=0123456789&bankcode=000013'));
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
  "account_name": "AKINDELE CHIOMA HASSAN",
  "msg": "Account name resolved"
}
```
{% endcode %}
