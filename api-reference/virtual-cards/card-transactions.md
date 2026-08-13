# Card Transactions

Get the transaction history for a specific virtual card.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/vcard-trans`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field     | Type   | Required | Description   |
| --------- | ------ | -------- | ------------- |
| `vcardid` | string | Yes      | The card's ID |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/vcard-trans' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data '{
    "vcardid": "ao022-22e23o-2238-2829d"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/vcard-trans', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ vcardid: 'ao022-22e23o-2238-2829d' })
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
  "vcardid": "ao022-22e23o-2238-2829d"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/vcard-trans'
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

url = "{{base_url}}/business/vcard-trans"

payload = json.dumps({'vcardid': 'ao022-22e23o-2238-2829d'})
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
  CURLOPT_URL => '{{base_url}}/business/vcard-trans',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "vcardid": "ao022-22e23o-2238-2829d"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/vcard-trans'));
request.body = json.encode({
  "vcardid": "ao022-22e23o-2238-2829d"
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
  "msg": "Transaction Retrieved",
  "data": [
    {
      "card_type": "virtual",
      "card_brand": "Mastercard",
      "card_currency": "USD",
      "maskedPan": "501300********1234",
      "amount": 38,
      "fee": "0",
      "merchant_name": "Facebook. Sub",
      "merchant_city": "6007100 MA",
      "description": "Approved or completed successfully",
      "transtype": "Settlement",
      "transtatus": "1",
      "trans_reference": 18050757,
      "transdate": "2024-11-08T03:44:13"
    },
    {
      "card_type": "virtual",
      "card_brand": "Mastercard",
      "card_currency": "USD",
      "maskedPan": "501300********1234",
      "amount": 40,
      "fee": "0",
      "merchant_name": "Boldd",
      "description": "Card Funding of 40",
      "transtype": "CardFunding",
      "transtatus": "1",
      "trans_reference": 0,
      "transdate": "2024-11-07T14:48:17"
    }
  ]
}
```
{% endcode %}
