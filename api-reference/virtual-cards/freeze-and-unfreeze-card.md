# Freeze and Unfreeze Card

Disable or re-enable a card. This single endpoint works for **both virtual and physical cards**  the field is still named `vcardid` regardless of card type.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/vcard-update.php` (or `POST {{base_url}}/business/vcard-update`)

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field        | Type   | Required | Description                                  |
| ------------ | ------ | -------- | -------------------------------------------- |
| `cardid`     | string | Yes      | The card's ID (`cardid` or `vcardid`)        |
| `updatetype` | string | Yes      | `freeze` to disable, `unfreeze` to re-enable |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/vcard-update' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data '{
    "vcardid": "ao022-22e23o-2238-2829d",
    "updatetype": "freeze"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/vcard-update', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ vcardid: 'ao022-22e23o-2238-2829d', updatetype: 'freeze' })
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
  "vcardid": "ao022-22e23o-2238-2829d",
  "updatetype": "freeze"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/vcard-update'
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

url = "{{base_url}}/business/vcard-update"

payload = json.dumps({'vcardid': 'ao022-22e23o-2238-2829d', 'updatetype': 'freeze'})
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
  CURLOPT_URL => '{{base_url}}/business/vcard-update',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "vcardid": "ao022-22e23o-2238-2829d",
    "updatetype": "freeze"
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/vcard-update'));
request.body = json.encode({
  "vcardid": "ao022-22e23o-2238-2829d",
  "updatetype": "freeze"
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

```json
{
  "status": true,
  "responsecode": "01",
  "message": "Card successfully updated"
}
```

```json
{
  "status": false,
  "responsecode": "00",
  "message": "Unable to process request"
}
```

### Freeze & Unfreeze Behavior

* **`updatetype: "freeze"`**: Immediately disables the virtual card from making further transactions or withdrawals.
* **`updatetype: "unfreeze"`**: Re-enables the card, allowing funding, withdrawals, and online transactions to resume if eligible.
* Accepts either `cardid` or `vcardid` in the request payload.
