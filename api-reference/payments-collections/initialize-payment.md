# Initialize Payment

Start a new payment link transaction. Boldd returns a hosted checkout URL to redirect your customer to.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/initiatetrans`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field            | Type   | Required | Description                                                                              |
| ---------------- | ------ | -------- | ---------------------------------------------------------------------------------------- |
| `amount`         | string | Yes      | Transaction amount                                                                       |
| `fname`          | string | Yes      | Customer's first name                                                                    |
| `lname`          | string | Yes      | Customer's last name                                                                     |
| `customer_email` | string | Yes      | Customer's email                                                                         |
| `phone`          | string | Yes      | Customer's phone number                                                                  |
| `reference`      | string | Yes      | Your unique transaction reference                                                        |
| `currency`       | string | Yes      | `NGN`, `GHS`, `ZAR`, or `USD`                                                            |
| `redirecturl`    | string | No       | Where the customer is sent after paying                                                  |
| `meta_data`      | object | No       | Extra context — subaccount routing, commission overrides, cart/order details (see below) |

**`meta_data` example**

```json
{
  "meta_data": {
    "subaccount": true,
    "trackingid": "T3131122122",
    "inflowcomm": "0.3",
    "order_id": 570,
    "cart_id": 335,
    "tx_id": 518,
    "vat": "0",
    "storedata": [
      {
        "name": "Another Clothing",
        "products": [
          { "product_id": 285, "description": "Gorilla T-shirt", "quantity": 1, "amount": 50000 }
        ]
      }
    ]
  }
}
```

{% hint style="info" %}
Leave `inflowcomm` empty to use your default dashboard commission fee, or pass `0` to charge nothing extra.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request POST '{{base_url}}/business/initiatetrans' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "amount": "500",
    "fname": "John",
    "lname": "Doe",
    "customer_email": "example@gmail.com",
    "phone": "09012345678",
    "reference": "fghjkl56789g",
    "currency": "NGN",
    "redirecturl": "https://example.com"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/initiatetrans', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    amount: '500',
    fname: 'John',
    lname: 'Doe',
    customer_email: 'example@gmail.com',
    phone: '09012345678',
    reference: 'fghjkl56789g',
    currency: 'NGN',
    redirecturl: 'https://example.com'
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
    "amount": "500",
    "fname": "John",
    "lname": "Doe",
    "customer_email": "example@gmail.com",
    "phone": "09012345678",
    "reference": "fghjkl56789g",
    "currency": "NGN",
    "redirecturl": "https://example.com"
  });

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/initiatetrans',
  headers: { 
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
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

url = "{{base_url}}/business/initiatetrans"

payload = json.dumps({'amount': '500', 'fname': 'John', 'lname': 'Doe', 'customer_email': 'example@gmail.com', 'phone': '09012345678', 'reference': 'fghjkl56789g', 'currency': 'NGN', 'redirecturl': 'https://example.com'})
headers = {
  'Authorization': 'Bearer YOUR_SECRET_KEY',
  'Content-Type': 'application/json'
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
  CURLOPT_URL => '{{base_url}}/business/initiatetrans',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "amount": "500",
    "fname": "John",
    "lname": "Doe",
    "customer_email": "example@gmail.com",
    "phone": "09012345678",
    "reference": "fghjkl56789g",
    "currency": "NGN",
    "redirecturl": "https://example.com"
}',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer YOUR_SECRET_KEY',
    'Content-Type: application/json'
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
  'Authorization': 'Bearer YOUR_SECRET_KEY',
  'Content-Type': 'application/json'
};
var request = http.Request('POST', Uri.parse('{{base_url}}/business/initiatetrans'));
request.body = json.encode({'amount': '500', 'fname': 'John', 'lname': 'Doe', 'customer_email': 'example@gmail.com', 'phone': '09012345678', 'reference': 'fghjkl56789g', 'currency': 'NGN', 'redirecturl': 'https://example.com'});
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
  "message": "Successful",
  "reference": "2345KDF12",
  "access_token": "6983b68c269f7fgha2beb85625288",
  "authorization_url": "https://pay.oneappgo.com/checkout/6983b68c269f7fgha2beb85625288/63490b1643375660547"
}
```
{% endcode %}

Redirect your customer to `authorization_url` to complete payment. After payment, they land back on your `redirecturl`. Always confirm the outcome server-side with **Verify Payment** — don't rely on the redirect alone.
