# Create Customer (Full KYC)

Full KYC is required before creating physical cards, virtual cards, or Global Accounts for a customer.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/fullkyc-customer`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field               | Type   | Required | Description                                                                     |
| ------------------- | ------ | -------- | ------------------------------------------------------------------------------- |
| `first_name`        | string | Yes      | Customer first name                                                             |
| `last_name`         | string | Yes      | Customer last name                                                              |
| `middle_name`       | string | No       |                                                                                 |
| `email_address`     | string | Yes      | Customer email                                                                  |
| `phone_number`      | string | Yes      | e.g. `+2347012345689`                                                           |
| `birth_date`        | string | Yes      | Format `yyyy-mm-dd`. Customer must be at least 18                               |
| `nationality`       | string | Yes      | ISO 3166-1 three-character country code, e.g. `NGR`                             |
| `gender`            | string | Yes      | `male` or `female`                                                              |
| `bvnno`             | string | Yes      | Customer BVN                                                                    |
| `taxno`             | string | No       |                                                                                 |
| `employment_status` | string | Yes      | `employed`, `homemaker`, `retired`, `self_employed`, `student`, or `unemployed` |
| `address`           | object | Yes      | See sample below                                                                |
| `identity`          | object | Yes      | See sample below                                                                |

**Identity types:** `PASSPORT`, `NIN`, `DRIVER_LICENSE`, `VOTER_CARD`, `NATIONAL_IDENTITY`

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location '{{base_url}}/business/fullkyc-customer' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--data-raw '{
    "first_name": "John",
    "last_name": "Doe",
    "middle_name": "Faith",
    "phone_number": "07012345678",
    "bvnno": "20123456780",
    "birth_date": "2000-03-23",
    "nationality": "NGR",
    "gender": "male",
    "employment_status": "employed",
    "email_address": "email@example.com",
    "taxno": "29323239D2",
    "address": {
        "house_no": "5",
        "street": "Queen Estate, Alen Road",
        "city": "Ikeja",
        "state": "Lagos State",
        "country": "Nigeria",
        "postal_code": "110320"
    },
    "identity": {
        "idtype": "NATIONAL_IDENTITY",
        "idno": "24H675B9084",
        "expiry_date": "2030-01-01",
        "idfront_url": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
        "idback_url": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
        "issuance_country": "Nigeria"
    }
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/fullkyc-customer', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    first_name: 'John',
    last_name: 'Doe',
    middle_name: 'Faith',
    phone_number: '07012345678',
    bvnno: '20123456780',
    birth_date: '2000-03-23',
    nationality: 'NGR',
    gender: 'male',
    employment_status: 'employed',
    email_address: 'email@example.com',
    taxno: '29323239D2',
    address: {
      house_no: '5',
      street: 'Queen Estate, Alen Road',
      city: 'Ikeja',
      state: 'Lagos State',
      country: 'Nigeria',
      postal_code: '110320'
    },
    identity: {
      idtype: 'NATIONAL_IDENTITY',
      idno: '24H675B9084',
      expiry_date: '2030-01-01',
      idfront_url: 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png',
      idback_url: 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png',
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
  "birth_date": "2000-03-23",
  "nationality": "NGR",
  "middle_name": "Faith",
  "gender": "male",
  "employment_status": "EMPLOYED",
  "email_address": "email@example.com",
  "taxno": "29323239D2",
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
    "expiry_date": "24H675B9084",
        "idfront_url": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
        "idback_url": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
    "issuance_country": "Nigeria"
  }
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: '{{base_url}}/business/fullkyc-customer',
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

url = "{{base_url}}/business/fullkyc-customer"

payload = json.dumps({'first_name': 'John', 'last_name': 'Doe', 'middle_name': 'Faith', 'phone_number': '07012345678', 'bvnno': '20123456780', 'birth_date': '2000-03-23', 'nationality': 'NGR', 'gender': 'male', 'employment_status': 'employed', 'email_address': 'email@example.com', 'taxno': '29323239D2', 'address': {'house_no': '5', 'street': 'Queen Estate, Alen Road', 'city': 'Ikeja', 'state': 'Lagos State', 'country': 'Nigeria', 'postal_code': '110320'}, 'identity': {'idtype': 'NATIONAL_IDENTITY', 'idno': '24H675B9084', 'expiry_date': '2030-01-01', 'idfront_url': 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png', 'idback_url': 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png', 'issuance_country': 'Nigeria'}})
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
  CURLOPT_URL => '{{base_url}}/business/fullkyc-customer',
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
    "middle_name": "Faith",
    "phone_number": "07012345678",
    "bvnno": "20123456780",
    "birth_date": "2000-03-23",
    "nationality": "NGR",
    "gender": "male",
    "employment_status": "employed",
    "email_address": "email@example.com",
    "taxno": "29323239D2",
    "address": {
        "house_no": "5",
        "street": "Queen Estate, Alen Road",
        "city": "Ikeja",
        "state": "Lagos State",
        "country": "Nigeria",
        "postal_code": "110320"
    },
    "identity": {
        "idtype": "NATIONAL_IDENTITY",
        "idno": "24H675B9084",
        "expiry_date": "2030-01-01",
        "idfront_url": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
        "idback_url": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
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
var request = http.Request('POST', Uri.parse('{{base_url}}/business/fullkyc-customer'));
request.body = json.encode({
  "first_name": "John",
  "last_name": "Doe",
  "phone_number": "07012345678",
  "bvnno": "20123456780",
  "birth_date": "2000-03-23",
  "nationality": "NGR",
  "middle_name": "Faith",
  "gender": "male",
  "employment_status": "EMPLOYED",
  "email_address": "email@example.com",
  "taxno": "29323239D2",
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
    "expiry_date": "24H675B9084",
        "idfront_url": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
        "idback_url": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png",
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

{% tabs %}
{% tab title="Success" %}
```json
{
  "status": true,
  "responsecode": "01",
  "message": "Customer account fully created for John Doe",
  "trackid": "06211211"
}
```
{% endtab %}

{% tab title="Failure" %}
```json
{
  "status": false,
  "responsecode": "00",
  "message": "Unable to process request. Invalid authorization key",
  "trackid": ""
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Review:** the legacy docs' sample `expiry_date` value (`"24H675B9084"`) is clearly copy-pasted from the `idno` field above it — replaced here with a plausible date format. Confirm the actual expected `expiry_date` format with the API team.
{% endhint %}
