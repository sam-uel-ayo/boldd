# Get Exchange Rate

Fetch the current exchange rate between two currencies, along with the minimum and maximum convertible amounts. Requires the `ngnusd`, `currencyswap`, or `currencyexchange` service grant (see **Service Access & Limits**).

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/rate.php` (or `POST {{base_url}}/business/rate`)

**Request Headers**

| Header          | Type     | Required | Description                                                                              |
| --------------- | -------- | -------- | ---------------------------------------------------------------------------------------- |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY` or `Bearer YOUR_PUBLIC_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).                                           |

#### Service Grant & Currency Swap Access

* **Service Grant Name:** `ngnusd` (also configured as `currencyswap` or `currencyexchange` in admin).
* **Access Rule:** To query live exchange rates and perform currency swaps, the business account must have the `ngnusd` service grant enabled in admin.

#### Request Body

| Field          | Type   | Required | Description                                       |
| -------------- | ------ | -------- | ------------------------------------------------- |
| `currencypair` | string | Yes      | Six-letter currency pair, e.g. `USDNGN`, `NGNKES` |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/rate' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_PUBLIC_KEY' \
--data '{
    "currencypair": "USDNGN"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/rate', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_PUBLIC_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ currencypair: 'USDNGN' })
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
  "currencypair": "NGNKES"
});

let config = {
  method: 'post',
  url: '{{base_url}}/business/rate',
  headers: { 
    'Content-Type': 'application/json', 
    'Authorization': 'Bearer YOUR_PUBLIC_KEY', 
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

url = "{{base_url}}/business/rate"

payload = json.dumps({'currencypair': 'USDNGN'})
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer YOUR_PUBLIC_KEY'
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
  CURLOPT_URL => '{{base_url}}/business/rate',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "currencypair": "USDNGN"
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json',
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
```
var headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer YOUR_PUBLIC_KEY'
};
var request = http.Request('POST', Uri.parse('{{base_url}}/business/rate'));
request.body = json.encode({
  "currencypair": "USDNGN"
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

#### Sample response

{% code title="Sample response" overflow="wrap" %}
```json
{
  "status": true,
  "message": "Exchange rate fetched successfully",
  "data": {
    "minAmount": 0.1,
    "maxAmount": 10000,
    "exchangeRate": 1429
  }
}
```
{% endcode %}
