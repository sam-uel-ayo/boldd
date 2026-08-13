# Fetch Disputes

Retrieve all chargeback/fraud disputes logged against your account.

**Endpoint**

<mark style="color:blue;">`GET`</mark> `{{base_url}}/business/disputes`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET '{{base_url}}/business/disputes' \
--header 'Authorization: Bearer YOUR_SECRET_KEY'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/disputes', {
  headers: { 'Authorization': 'Bearer YOUR_SECRET_KEY' }
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Node.js (Axios)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'GET',
  'hostname': 'api.oneappgo.com',
  'path': '/v1/business/disputes',
  'headers': {
    'Authorization': 'Bearer YOUR_SECRET_KEY'
  },
  'maxRedirects': 20
};

var req = https.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function (chunk) {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });

  res.on("error", function (error) {
    console.error(error);
  });
});

req.end();
```
{% endcode %}
{% endtab %}

{% tab title="Python (Requests)" %}
{% code overflow="wrap" lineNumbers="true" %}
```python
import requests

url = "{{base_url}}/business/disputes"

payload={}
headers = {
  'Authorization': 'Bearer YOUR_SECRET_KEY'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```
{% endcode %}
{% endtab %}

{% tab title="PHP (cURL)" %}
{% code overflow="wrap" lineNumbers="true" %}
```php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => '{{base_url}}/business/disputes',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_POSTFIELDS =>'{{base_url}}',
  CURLOPT_HTTPHEADER => array(
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
  'Authorization': 'Bearer YOUR_SECRET_KEY'
};
var request = http.Request('GET', Uri.parse('{{base_url}}/business/disputes'));
request.body = '{{base_url}}';
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
  "message": "Dispute retrieved",
  "disputecount": 2,
  "data": [
    {
      "disputeid": "5",
      "transref": "83810B1637657021448",
      "amount": "100.00",
      "customer": "example@gmail.com",
      "gateway": "transfer",
      "type": "chargeback",
      "logged_date": "1639999861",
      "duedate": "25 Dec 2021 12:00 am",
      "statuscode": "0",
      "statustext": "Declined"
    },
    {
      "disputeid": "4",
      "transref": "83810B1637750693902",
      "amount": "100.00",
      "customer": "example2@gmail.com",
      "gateway": "transfer",
      "type": "fraud",
      "logged_date": "1639999843",
      "duedate": "22 Dec 2021 12:00 am",
      "statuscode": "1",
      "statustext": "Awaiting Response"
    }
  ]
}
```
{% endcode %}

Respond to an open dispute using **Accept a Dispute** or **Decline a Dispute** before its `duedate`.
