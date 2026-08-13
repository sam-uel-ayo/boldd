# Card Request Status

Track fulfillment of a virtual card request, or recover the response if you missed it originally.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/vcard-request-status`

**Request Headers**

<table><thead><tr><th width="141.6666259765625">Header</th><th>Type</th><th>Required</th><th>Description</th></tr></thead><tbody><tr><td><code>Authorization</code></td><td><code>String</code></td><td>Yes</td><td>Bearer token authentication (e.g. <code>Bearer YOUR_SECRET_KEY</code>).</td></tr><tr><td><code>Content-Type</code></td><td><code>String</code></td><td>Yes</td><td>Request body format (e.g. <code>application/json</code>).</td></tr></tbody></table>

#### Request Body

| Field       | Type   | Required | Description                                   |
| ----------- | ------ | -------- | --------------------------------------------- |
| `requestid` | string | Yes      | The `requestid` returned from **Create Card** |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/vcard-request-status' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data-raw '{
    "requestid": "06211-21140-12129-12329"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/cardrequest-status', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ requestid: '06211-21140-12129-12329' })
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
  "requestid": "06211-21140-12129-12329"
});

let config = {
  method: 'GET',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/cardrequest-status',
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

url = "{{base_url}}/business/cardrequest-status"

payload = json.dumps({'requestid': '06211-21140-12129-12329'})
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
  CURLOPT_URL => '{{base_url}}/business/cardrequest-status',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "requestid": "06211-21140-12129-12329"
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
var request = http.Request('GET', Uri.parse('{{base_url}}/business/cardrequest-status'));
request.body = json.encode({
  "requestid": "06211-21140-12129-12329"
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
  "requeststatus": "processing",
  "message": "Card request processing",
  "data": []
}
```
{% endtab %}

{% tab title="Failure" %}
```json
{
  "status": false,
  "responsecode": "00"
}
```
{% endtab %}
{% endtabs %}

`requeststatus` moves through states such as `processing` → `provisioned` as the physical card is manufactured and shipped.

