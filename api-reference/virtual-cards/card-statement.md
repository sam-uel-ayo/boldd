# Card Statement

Get the full transaction statement for a card.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/card-statement`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field    | Type   | Required | Description   |
| -------- | ------ | -------- | ------------- |
| `cardid` | string | Yes      | The card's ID |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/card-statement' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data '{
    "cardid": "ao022-22e23o-2238-2829d"
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
  body: JSON.stringify({ cardid: 'ao022-22e23o-2238-2829d' })
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
  "cardid": "ao022-22e23o-2238-2829d"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/card-statement'
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

payload = json.dumps({'cardid': 'ao022-22e23o-2238-2829d'})
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
    "cardid": "ao022-22e23o-2238-2829d"
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
  "cardid": "ao022-22e23o-2238-2829d"
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
**Review:** in the original combined sidebar draft, **Card Statement** and **Update Card PIN** were listed under Virtual Cards. In the actual source content, both endpoints only ever appear under the Physical Card section, and neither uses a `vcardid`-style field — they use the generic `cardid` field also used by other physical-card endpoints. Placed here under Physical Cards to match the documented content; worth confirming with the API team whether they also work for virtual cards before deciding whether to cross-list them.
{% endhint %}
