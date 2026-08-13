# Create Card Account

Create the underlying card-holder profile for a customer before issuing their first card. Returns a `trackid` used for issuance.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/createcard-customer`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field           | Type   | Required | Description           |
| --------------- | ------ | -------- | --------------------- |
| `first_name`    | string | Yes      | Customer first name   |
| `last_name`     | string | Yes      | Customer last name    |
| `email_address` | string | Yes      | Customer email        |
| `phone_number`  | string | Yes      | Customer phone number |
| `bvnno`         | string | Yes      | Customer BVN          |
| `address`       | object | Yes      | See sample below      |
| `identity`      | object | Yes      | See sample below      |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/createcard-customer' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data-raw '{
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "07012345678",
    "bvnno": "20123456780",
    "email_address": "email@example.com",
    "address": {
        "house_no": "5",
        "street": "Queen Estate, Alen Road",
        "city": "Ikeja",
        "state": "Lagos State",
        "country": "Nigeria",
        "postal_code": "2323"
    },
    "identity": {
        "idtype": "NATIONAL_IDENTITY",
        "idno": "24H675B9084",
        "idurl": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
        "issuance_country": "Nigeria"
    }
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/createcard-customer', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    first_name: 'John',
    last_name: 'Doe',
    phone_number: '07012345678',
    bvnno: '20123456780',
    email_address: 'email@example.com',
    address: {
      house_no: '5', street: 'Queen Estate, Alen Road', city: 'Ikeja',
      state: 'Lagos State', country: 'Nigeria', postal_code: '2323'
    },
    identity: {
      idtype: 'NATIONAL_IDENTITY', idno: '24H675B9084',
      idurl: 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png',
      issuance_country: 'Nigeria'
    }
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
  "first_name": "John",
  "last_name": "Doe",
  "phone_number": "07012345678",
  "bvnno": "20123456780",
  "email_address": "email@example.com",
  "address": {
    "house_no": "5",
    "street": "queen Estate, Alen road",
    "city": "Ikeja",
    "state": "Lagos State",
    "country": "Nigeria",
    "postal_code": "2323"
  },
  "identity": {
    "idtype": "National identity",
    "idno": "24H675B9084",
    "idurl": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
    "issuance_country": "Nigeria"
  }
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/createcard-customer',
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

url = "{{base_url}}/business/createcard-customer"

payload = json.dumps({'first_name': 'John', 'last_name': 'Doe', 'phone_number': '07012345678', 'bvnno': '20123456780', 'email_address': 'email@example.com', 'address': {'house_no': '5', 'street': 'Queen Estate, Alen Road', 'city': 'Ikeja', 'state': 'Lagos State', 'country': 'Nigeria', 'postal_code': '2323'}, 'identity': {'idtype': 'NATIONAL_IDENTITY', 'idno': '24H675B9084', 'idurl': 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png', 'issuance_country': 'Nigeria'}})
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
  CURLOPT_URL => '{{base_url}}/business/createcard-customer',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "07012345678",
    "bvnno": "20123456780",
    "email_address": "email@example.com",
    "address": {
        "house_no": "5",
        "street": "Queen Estate, Alen Road",
        "city": "Ikeja",
        "state": "Lagos State",
        "country": "Nigeria",
        "postal_code": "2323"
    },
    "identity": {
        "idtype": "NATIONAL_IDENTITY",
        "idno": "24H675B9084",
        "idurl": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
        "issuance_country": "Nigeria"
    }
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/createcard-customer'));
request.body = json.encode({
  "first_name": "John",
  "last_name": "Doe",
  "phone_number": "07012345678",
  "bvnno": "20123456780",
  "email_address": "email@example.com",
  "address": {
    "house_no": "5",
    "street": "queen Estate, Alen road",
    "city": "Ikeja",
    "state": "Lagos State",
    "country": "Nigeria",
    "postal_code": "2323"
  },
  "identity": {
    "idtype": "National identity",
    "idno": "24H675B9084",
    "idurl": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
    "issuance_country": "Nigeria"
  }
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
  "responsecode": "01",
  "message": "Card account successfully created for John Doe",
  "trackid": "06211211"
}
```
{% endcode %}
