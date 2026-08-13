# Buy Electricity

Vend electricity to a verified meter.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/electricity`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field       | Type   | Required | Description                                              |
| ----------- | ------ | -------- | -------------------------------------------------------- |
| `meterno`   | string | Yes      | From **Verify Meter Number**                             |
| `provider`  | string | Yes      | DisCo — same value used to verify                        |
| `amount`    | string | Yes      | Amount to vend                                           |
| `vendtype`  | string | Yes      | From **Verify Meter Number** response                    |
| `metername` | string | No       | Meter holder name, from **Verify Meter Number** response |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request POST '{{base_url}}/electricity' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "meterno": "62320094725",
    "metername": "IBRAHIM MARY OPE",
    "provider": "IBADAN",
    "amount": "10000",
    "vendtype": "PREPAID"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/electricity', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ meterno: '62320094725', metername: 'IBRAHIM MARY OPE', provider: 'IBADAN', amount: '10000', vendtype: 'PREPAID' })
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
    "meterno": "62320094725",
    "metername": "IBRAHIM MARY OPE",
    "provider": "IBADAN",
    "amount": "10000",
    "vendtype": "PREPAID"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/electricity',
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

url = "{{base_url}}/electricity"

payload = json.dumps({'meterno': '62320094725', 'metername': 'IBRAHIM MARY OPE', 'provider': 'IBADAN', 'amount': '10000', 'vendtype': 'PREPAID'})
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
  CURLOPT_URL => '{{base_url}}/electricity',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "meterno": "62320094725",
    "metername": "IBRAHIM MARY OPE",
    "provider": "IBADAN",
    "amount": "10000",
    "vendtype": "PREPAID"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/electricity'));
request.body = json.encode({'meterno': '62320094725', 'metername': 'IBRAHIM MARY OPE', 'provider': 'IBADAN', 'amount': '10000', 'vendtype': 'PREPAID'});
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
  "message": "Success - Bills Payment effected successfully - Token: 0283-6213-2450-8322-0153",
  "txref": "API2650280812e8401",
  "charged": 10030,
  "token": "0283-6213-2450-8322-0153",
  "newbal": 300094.79
}
```
{% endcode %}

For prepaid meters, `token` is the recharge token the customer enters on their meter.

{% hint style="info" %}
**Review:** the legacy docs' request-body table also lists `pckgid` and `address` as required fields, but no working sample request anywhere actually includes them, and both fields are absent from the Postman collection's saved example. Left out of the body here to match what's actually been demonstrated working — confirm with the API team whether they're truly required.
{% endhint %}
