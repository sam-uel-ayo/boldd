# Cards Details

Get a card's status and balance **without** exposing the full card number or CVV. Safe to use in contexts you don't want raw PAN data flowing through.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/vcard-details`

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
curl --location '{{base_url}}/business/vcard-details' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data '{
    "cardid": "021109a9-4bfa-4321-02ca-dc91e9a7b4"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/vcard-details', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ cardid: '021109a9-4bfa-4321-02ca-dc91e9a7b4' })
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
  "cardid": "021109a9-4bfa-4321-02ca-dc91e9a7b4"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/carddetails'
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

url = "{{base_url}}/business/vcard-details"

payload = json.dumps({'cardid': '021109a9-4bfa-4321-02ca-dc91e9a7b4'})
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
  CURLOPT_URL => '{{base_url}}/business/vcard-details',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "cardid": "021109a9-4bfa-4321-02ca-dc91e9a7b4"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/carddetails'));
request.body = json.encode({
  "cardid": "021109a9-4bfa-4321-02ca-dc91e9a7b4"
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
  "message": "Card info retrieved",
  "billingAddress": {
    "line1": "Oyo State", "line2": "", "city": "Ibadan",
    "state": "Oyo", "country": "NG", "postalCode": "201231"
  },
  "current_bal": 112.27,
  "available_bal": 112.27,
  "responsecode": "01",
  "cardstatus": "active",
  "holdertype": "individual",
  "cardbrand": "MASTERCARD",
  "cardtype": "Virtual",
  "cardpan": "583007********0000",
  "expiryyr": "27",
  "expirymnt": "06",
  "holdername": "John Doe",
  "customerid": "01057-e48b-4e45-ddc1-0c91ec1988",
  "card_id": "021109a9-4bfa-4321-02ca-dc91e9a7b4",
  "currency": "USD",
  "created_at": "Sat, 22-06-2024 09:08 pm",
  "dstatus": "1",
  "defaultpin": "****"
}
```
{% endcode %}

If a request is missing `cardid`, the response includes `missing_fields` and `received_fields` per the standard error envelope. See **Response Code & Errors**.

Use this endpoint if a create-card request succeeded but you never received the response - refetch and store the card payload locally to complete the missing record.
