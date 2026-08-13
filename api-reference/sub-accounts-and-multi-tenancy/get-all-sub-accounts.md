# Get All Sub-Accounts

List every sub-account under your business, with balances and status.

**Endpoint**

<mark style="color:blue;">`GET`</mark> `{{base_url}}/business/subaccounts`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/subaccounts' \
--header 'Authorization: Bearer YOUR_SECRET_KEY'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/subaccounts', {
  headers: { 'Authorization': 'Bearer YOUR_SECRET_KEY' }
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Node.js (Axios)" %}
{% code overflow="wrap" lineNumbers="true" %}
```json
const axios = require('axios');

let config = {
  method: 'get',
  url: '{{base_url}}/business/subaccounts',
  headers: { 
    'Authorization': 'Bearer YOUR_SECRET_KEY',
  }
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

url = "{{base_url}}/business/subaccounts"

payload = '{{base_url}}'
headers = {
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
  CURLOPT_URL => '{{base_url}}/business/subaccounts',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/subaccounts'));
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
  "message": "Success",
  "data": [
    {
      "name": "Olamide Kabiru",
      "email": "ojid@gmail.com",
      "phoneno": "09010029133",
      "balance": "800000.00",
      "customer_code": "",
      "tracking": "00109010029133",
      "smsalert": false,
      "date_created": "04, February 2025",
      "account_number": "",
      "bankname": "",
      "accountstatus": "Active"
    },
    {
      "name": "Olajide Olatunji",
      "email": "jide@test.com",
      "phoneno": "07068900000",
      "balance": "1000000.00",
      "customer_code": "00107068900000",
      "tracking": "00107068900000",
      "smsalert": true,
      "date_created": "30, May 2024",
      "account_number": "",
      "bankname": "",
      "accountstatus": "Active"
    }
  ]
}
```
{% endcode %}
