# Card Statement

Get the full transaction statement for both **Virtual Cards** and **Physical Cards**.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/card-statement` (or `card-statement.php`)

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `cardid` / `vcardid` | `string` | Yes | The card ID or virtual card ID to fetch statements for. |
| `from_date` | `string` | No | Start date for statement filter (`YYYY-MM-DD`). |
| `to_date` | `string` | No | End date for statement filter (`YYYY-MM-DD`). |
| `months` / `duration_months` | `number` | No | Number of months of statements to query (up to **3 months**; defaults to **1 month**). |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/card-statement' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data '{
    "cardid": "ao022-22e23o-2238-2829d",
    "months": 1
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/card-statement', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ 
    cardid: 'ao022-22e23o-2238-2829d',
    months: 1 
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
  "cardid": "ao022-22e23o-2238-2829d",
  "months": 1
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/card-statement',
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

url = "{{base_url}}/business/card-statement"

payload = json.dumps({
  'cardid': 'ao022-22e23o-2238-2829d',
  'months': 1
})
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
  CURLOPT_URL => '{{base_url}}/business/card-statement',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "cardid": "ao022-22e23o-2238-2829d",
    "months": 1
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/card-statement'));
request.body = json.encode({
  "cardid": "ao022-22e23o-2238-2829d",
  "months": 1
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
  "msg": "Transaction Statement",
  "data": [
    {
      "card_type": "physical",
      "card_brand": "Verve",
      "card_currency": "NGN",
      "amount": "38,000",
      "transchannel": "POS",
      "transtype": "Withdraw",
      "transtatus": "Success",
      "trans_reference": 180507920200022257,
      "transdate": "2024-11-08T03:44:13"
    }
  ]
}
```
{% endcode %}

{% hint style="info" %}
**Note:** `POST {{base_url}}/business/card-statement` supports both **Virtual Cards** and **Physical Cards**. It accepts either `cardid` or `vcardid`, defaults to the last 1 month, and supports date range filtering (`from_date`, `to_date`, `months`, `duration_months`) up to a maximum of **3 months**.
{% endhint %}
