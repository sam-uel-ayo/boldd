# Customers List

Retrieve every customer created under your business account, across both Tier 1 and Full KYC.

**Endpoint**

<mark style="color:blue;">`GET`</mark> `{{base_url}}/business/customers`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/customers' \
--header 'Authorization: Bearer YOUR_SECRET_KEY'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/customers', {
  headers: { 'Authorization': 'Bearer YOUR_SECRET_KEY' }
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Node.js (Axios)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({{base_url}});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/customers',
  headers: { 
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

url = "{{base_url}}/business/customers"

payload = '{{base_url}}'
headers = {
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
  CURLOPT_URL => '{{base_url}}/business/customers',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/customers'));
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
  "totalcustomer": 2,
  "message": "Customers retrieved",
  "data": [
    {
      "txref": "63490b145600340",
      "ctemail": "johndoe@gmail.com",
      "ctphone": "",
      "statuscode": "6",
      "customername": "John Doe"
    },
    {
      "txref": "634fghj93606583",
      "ctemail": "willsmith@gmail.com",
      "ctphone": "",
      "statuscode": "1",
      "customername": "Will Smith"
    }
  ]
}
```
{% endcode %}

### Customer Status Codes (`statuscode`)

The `statuscode` field on each customer record indicates the customer's current KYC verification level and status:

<table><thead><tr><th width="94.33331298828125">Code</th><th width="224.6666259765625">Status</th><th>Description</th></tr></thead><tbody><tr><td><code>1</code></td><td>Active / Full KYC</td><td>Customer is fully verified and active for all services (e.g. Virtual Accounts, USD Global Accounts).</td></tr><tr><td><code>6</code></td><td>Tier 1 / Partial KYC</td><td>Customer has completed basic Tier 1 verification (BVN/NIN) but pending Full KYC document submission.</td></tr><tr><td><code>0</code></td><td>Unverified / Pending</td><td>Customer profile created, but verification has not started.</td></tr><tr><td><code>2</code></td><td>Under Review</td><td>Customer KYC documents are submitted and currently under compliance review.</td></tr><tr><td><code>5</code></td><td>Deactivated / Suspended</td><td>Customer profile has been deactivated or restricted by compliance.</td></tr></tbody></table>

{% hint style="info" %}
Always ensure a customer has `statuscode: "1"` (Full KYC) before submitting a USD Global Account or Virtual Card request on their behalf.
{% endhint %}
