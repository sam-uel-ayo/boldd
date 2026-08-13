# Cards Issuance

Issue a new virtual card against a card account created above.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/vcard-issuance`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field        | Type   | Required | Description                                         |
| ------------ | ------ | -------- | --------------------------------------------------- |
| `trackingid` | string | Yes      | The `trackid` returned from **Create Card Account** |
| `cardbrand`  | string | Yes      | `Mastercard` or `Visa`                              |
| `currency`   | string | Yes      | `USD` or `NGN`                                      |
| `amount`     | number | Yes      | Amount to pre-fund the card with after issuing      |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/vcard-issuance' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data '{
    "currency": "USD",
    "trackingid": "9239293",
    "cardbrand": "Mastercard",
    "amount": 5
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/vcard-issuance', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ currency: 'USD', trackingid: '9239293', cardbrand: 'Mastercard', amount: 5 })
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
  "currency": "USD",
  "trackingid": "9239293",
  "cardbrand": "Mastercard",
  "amount": 5
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/vcard-issuance'
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

url = "{{base_url}}/business/vcard-issuance"

payload = json.dumps({'currency': 'USD', 'trackingid': '9239293', 'cardbrand': 'Mastercard', 'amount': 5})
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
  CURLOPT_URL => '{{base_url}}/business/vcard-issuance',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "currency": "USD",
    "trackingid": "9239293",
    "cardbrand": "Mastercard",
    "amount": 5
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/vcard-issuance'));
request.body = json.encode({
  "currency": "USD",
  "trackingid": "9239293",
  "cardbrand": "Mastercard",
  "amount": 5
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

{% tabs %}
{% tab title="Success" %}
```json
{
  "status": true,
  "responsecode": "01",
  "message": "Card Issuance Processing",
  "txref": "0621121102020",
  "charged": 6,
  "currency": "USD"
}
```
{% endtab %}

{% tab title="Failure" %}
```json
{
  "status": false,
  "responsecode": "00",
  "message": "Insufficient wallet balance for this transaction",
  "txref": "",
  "charged": ""
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Card issuance is asynchronous. When it finishes processing, you'll receive a webhook (`event_type: transactions`, `paid_through: virtualcard`) with the card details and card ID. If you miss it, use **Card Request Status** to recover it.
{% endhint %}
