# Data Bundle

Purchase a data bundle for a customer, using a `datacode` from **Data Plans**.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/databundle`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field        | Type   | Required | Description                                                         |
| ------------ | ------ | -------- | ------------------------------------------------------------------- |
| `network_id` | string | Yes      | See network table under **Airtime Purchase**                        |
| `datacode`   | string | Yes      | From **Data Plans**                                                 |
| `phoneno`    | string | Yes      | Recipient phone number                                              |
| `dtype`      | string | Yes      | `direct` or `sme` — matching the plan's `dtype` from **Data Plans** |
| `reference`  | string | No       | Your transaction reference                                          |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request POST '{{base_url}}/databundle' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "datacode": "1000",
    "network_id": "2",
    "phoneno": "07012345678",
    "dtype": "sme",
    "reference": "DJIEJ2MEUE2EN34"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/databundle', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ datacode: '1000', network_id: '2', phoneno: '07012345678', dtype: 'sme', reference: 'DJIEJ2MEUE2EN34' })
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
    "datacode": "1000",
    "network_id": "2",
    "phoneno": "07012345678",
    "dtype": "sme",
    "reference": "DJIEJ2MEUE2EN34"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/databundle',
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

url = "{{base_url}}/databundle"

payload = json.dumps({'datacode': '1000', 'network_id': '2', 'phoneno': '07012345678', 'dtype': 'sme', 'reference': 'DJIEJ2MEUE2EN34'})
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
  CURLOPT_URL => '{{base_url}}/databundle',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "datacode": "1000",
    "network_id": "2",
    "phoneno": "07012345678",
    "dtype": "sme",
    "reference": "DJIEJ2MEUE2EN34"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/databundle'));
request.body = json.encode({'datacode': '1000', 'network_id': '2', 'phoneno': '07012345678', 'dtype': 'sme', 'reference': 'DJIEJ2MEUE2EN34'});
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
  "txref": "API1090229525d60",
  "charged": "260.00",
  "newbal": 40083.79
}
```
{% endcode %}
