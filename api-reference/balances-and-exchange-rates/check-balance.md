# Check Balance

Retrieve your current wallet balance and linked account list.

**Endpoint**

<mark style="color:blue;">`GET`</mark> `{{base_url}}/balance`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET '{{base_url}}/balance' \
--header 'Authorization: Bearer YOUR_SECRET_KEY'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/balance', {
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
  url: '{{base_url}}/balance',
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

url = "{{base_url}}/balance"

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
  CURLOPT_URL => '{{base_url}}/balance',
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
var request = http.Request('GET', Uri.parse('{{base_url}}/balance'));
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

#### Response Fields

| Field           | Description                                  |
| --------------- | -------------------------------------------- |
| `available_bal` | Balance available for use                    |
| `ledger_bal`    | Full ledger balance, including pending items |
| `currency`      | Currency of the balance returned             |
| `acctlist`      | List of account numbers tied to this wallet  |

#### Sample response

{% code title="Sample response" overflow="wrap" %}
```json
{
  "status": true,
  "message": "Account Balance Retrieved",
  "ledger_bal": "0.00",
  "available_bal": "34602.11",
  "currency": "NGN",
  "acctlist": [
    {
      "bankname": "Providus Bank",
      "acctname": "BOLDD(John Doe)",
      "accountnumber": "1234567890"
    },
    {
      "bankname": "Fidelity Bank",
      "acctname": "John Doe",
      "accountnumber": "4550589796"
    }
  ]
}
```
{% endcode %}
